library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity TB_Add_Sub_4bit is
--  Port ( );
end TB_Add_Sub_4bit;

architecture Behavioral of TB_Add_Sub_4bit is
COMPONENT Add_Sub_4bit
     PORT(  A : in STD_LOGIC_VECTOR (3 downto 0); 
            B : in STD_LOGIC_VECTOR (3 downto 0); 
            S : out STD_LOGIC_VECTOR (3 downto 0);
            M : in STD_LOGIC;
            overflow : out STD_LOGIC );
END COMPONENT;


SIGNAL A,B,S : std_logic_vector (3 downto 0);
SIGNAL M, overflow : std_logic;

begin
UUT: Add_Sub_4bit PORT MAP(
    M => M,
    A => A, 
    B=>B,
    S => S,
    overflow => overflow
    );

process
 begin
     A <= "0101"; 
     B <= "1100";
     M <= '0';
     
 WAIT FOR 100 ns; -- after 100 ns change inputs
     A <="0010"; 
     B <= "1110";
     M <= '1';
 WAIT FOR 100 ns; --change again
     A <="1010"; 
     B <= "1010";
     M <= '1';
 WAIT FOR 100 ns; --change again
     A <= "1110"; 
     B <= "0001";
     M <= '1';
 WAIT FOR 100 ns;
     A <= "0110"; 
     B <= "1010";
     M <= '1';
 WAIT; -- will wait forever
end process;
end Behavioral;





