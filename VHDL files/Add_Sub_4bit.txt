library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity Add_Sub_4bit is
    Port ( A : in STD_LOGIC_VECTOR (3 downto 0); 
           B : in STD_LOGIC_VECTOR (3 downto 0); 
           S : out STD_LOGIC_VECTOR (3 downto 0);
           M : in STD_LOGIC;
           overflow : out STD_LOGIC);
end Add_Sub_4bit;

architecture Behavioral of Add_Sub_4bit is
component FA 
     port ( 
         A: in std_logic; 
         B: in std_logic; 
         C_in: in std_logic; 
         S: out std_logic; 
         C_out: out std_logic); 
 end component; 
 
 SIGNAL FA0_S, FA0_C, FA1_S, FA1_C, FA2_S, FA2_C, FA3_S, FA3_C, C_out : std_logic;
 Signal B0x , B1x , B2x , B3x : std_logic;
 
 
 
begin
B0x <= B(0) XOR M;
B1x <= B(1) XOR M;
B2x <= B(2) XOR M;
B3x <= B(3) XOR M;

FA_0 : FA 
 port map ( 
     A => A(0), 
     B => B0x, 
     C_in => M, 
     S => S(0), 
     C_Out => FA0_C);
  
FA_1 : FA 
 port map ( 
     A => A(1), 
     B => B1x, 
     C_in => FA0_C, 
     S => S(1), 
     C_Out => FA1_C);
  
FA_2 : FA 
  port map ( 
      A => A(2), 
      B => B2x, 
      C_in => FA1_C, 
      S => S(2), 
      C_Out => FA2_C); 

FA_3 : FA 
  port map ( 
      A => A(3), 
      B => B3x, 
      C_in => FA2_C, 
      S => S(3), 
      C_Out => C_out
      );

overflow <= FA2_C xor C_out; 

end Behavioral;
