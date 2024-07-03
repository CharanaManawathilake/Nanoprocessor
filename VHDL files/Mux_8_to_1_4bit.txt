library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity Mux_8_to_1_4bit is
    Port ( S : in STD_LOGIC_VECTOR (2 downto 0);
           R0 : in STD_LOGIC_VECTOR (3 downto 0);
           R1 : in STD_LOGIC_VECTOR (3 downto 0);
           R2 : in STD_LOGIC_VECTOR (3 downto 0);
           R3 : in STD_LOGIC_VECTOR (3 downto 0);
           R4 : in STD_LOGIC_VECTOR (3 downto 0);
           R5 : in STD_LOGIC_VECTOR (3 downto 0);
           R6 : in STD_LOGIC_VECTOR (3 downto 0);
           R7 : in STD_LOGIC_VECTOR (3 downto 0);
           Q : out STD_LOGIC_VECTOR (3 downto 0));
end Mux_8_to_1_4bit;

architecture Behavioral of Mux_8_to_1_4bit is
    component Decoder_3_to_8
        port(
            I : in std_logic_vector;
            EN : in std_logic;
            Y : out std_logic_vector);
    end component;
    signal I0 : std_logic_vector (2 downto 0);
    signal EN0 : std_logic;
    signal X: std_logic_vector (7 downto 0);
    
begin
    Decoder_3_to_8_0 : Decoder_3_to_8
        port map(
            I => I0,
            EN => EN0,
            Y => X);
    EN0 <= '1';
    I0 <= S;
    Q(0) <= (R0(0) AND X(0)) OR (R1(0) AND X(1)) OR (R2(0) AND X(2)) OR (R3(0) AND X(3)) OR (R4(0) AND X(4)) OR (R5(0) AND X(5)) OR (R6(0) AND X(6)) OR (R7(0) AND X(7)); 
    Q(1) <= (R0(1) AND X(0)) OR (R1(1) AND X(1)) OR (R2(1) AND X(2)) OR (R3(1) AND X(3)) OR (R4(1) AND X(4)) OR (R5(1) AND X(5)) OR (R6(1) AND X(6)) OR (R7(1) AND X(7)); 
    Q(2) <= (R0(2) AND X(0)) OR (R1(2) AND X(1)) OR (R2(2) AND X(2)) OR (R3(2) AND X(3)) OR (R4(2) AND X(4)) OR (R5(2) AND X(5)) OR (R6(2) AND X(6)) OR (R7(2) AND X(7)); 
    Q(3) <= (R0(3) AND X(0)) OR (R1(3) AND X(1)) OR (R2(3) AND X(2)) OR (R3(3) AND X(3)) OR (R4(3) AND X(4)) OR (R5(3) AND X(5)) OR (R6(3) AND X(6)) OR (R7(3) AND X(7)); 
      
end Behavioral;
