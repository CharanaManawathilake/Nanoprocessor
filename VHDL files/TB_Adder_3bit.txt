library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity TB_Adder_3bit is
--  Port ( );
end TB_Adder_3bit;

architecture Behavioral of TB_Adder_3bit is
COMPONENT Adder_3bit
 PORT(  A : IN STD_LOGIC_VECTOR (2 downto 0); 
        S: OUT STD_LOGIC_VECTOR (2 downto 0);
        carry : out STD_LOGIC );
END COMPONENT;

SIGNAL A : std_logic_vector (2 downto 0);
SIGNAL S: std_logic_vector (2 downto 0);
SIGNAL carry : std_logic;
begin
UUT: Adder_3bit PORT MAP(
    A(0) => A(0), 
    A(1) => A(1), 
    A(2)=> A(2), 
    S(0)=>S(0), S(1)=>S(1), S(2)=>S(2),
    carry  => carry
    );

process
 begin
     A(0) <= '1'; 
     A(1) <= '0';
     A(2) <= '1';
 WAIT FOR 100 ns; -- after 100 ns change inputs
     A(0) <= '1'; 
     A(1) <= '1';
     A(2) <= '1';
 WAIT FOR 100 ns; --change again
    A(0) <= '0'; 
    A(1) <= '0';
    A(2) <= '1';
 WAIT FOR 100 ns; --change again
    A(0) <= '0'; 
    A(1) <= '1';
    A(2) <= '1';
 WAIT ;
 
end process;
end Behavioral;
