# 4-to-1-Multiplexer

Here it is from the combinational logic circuit example multiplexer (a device that selects between a number of input signals)  Depending on the values of the selection lines (s1, s0), it routes one of the input data signals (d0, d1, d2, d3) to the output (y).

RTL CODE:
module mux4to1 (
    input wire d0,d1,d2,d3   
    input wire s0,s1 
    output reg y    
);

always @(*) begin
    case ({s1, s0})  
        2'b00: y = d0;
        2'b01: y = d1;
        2'b10: y = d2;
        2'b11: y = d3;
        default: y = 1'b0;  
    endcase
end
endmodule

TESTBENCH CODE:
module tb_mux4to1;

reg d0, d1, d2, d3;
reg s0, s1;
wire y;

// Instantiate the 4-to-1 multiplexer
mux4to1 uut (
    .d0(d0),
    .d1(d1),
    .d2(d2),
    .d3(d3),
    .s0(s0),
    .s1(s1),
    .y(y)
);


initial 
  begin
    d0 = 0; d1 = 1; d2 = 0; d3 = 1;
    s0 = 0; s1 = 0;
    #10; 
    $display("s1 = %b, s0 = %b, y = %b (Expected y = d0)", s1, s0, y);
    s0 = 1; s1 = 0;
    #10;
    $display("s1 = %b, s0 = %b, y = %b (Expected y = d1)", s1, s0, y);
    s0 = 0; s1 = 1;
    #10;
    $display("s1 = %b, s0 = %b, y = %b (Expected y = d2)", s1, s0, y);
    s0 = 1; s1 = 1;
    #10;
    $display("s1 = %b, s0 = %b, y = %b (Expected y = d3)", s1, s0, y);
    d0 = 1; d1 = 0; d2 = 1; d3 = 0;
    s0 = 0; s1 = 0;
    #10;
    $display("s1 = %b, s0 = %b, y = %b (Expected y = d0)", s1, s0, y); 
    $finish;
  end
endmodule
