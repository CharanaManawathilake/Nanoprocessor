

library IEEE;
use IEEE.STD_LOGIC_1164.ALL;


entity TB_Register_Bank is
--  Port ( );
end TB_Register_Bank;

architecture Behavioral of TB_Register_Bank is
    component Register_Bank is
        Port ( D : in STD_LOGIC_VECTOR ;
               Clk : in STD_LOGIC;
               I : in STD_LOGIC_VECTOR ;
               Clr : in STD_LOGIC;
               R1 : out STD_LOGIC_VECTOR;
               R2 : out STD_LOGIC_VECTOR ;
               R3 : out STD_LOGIC_VECTOR ;
               R4 : out STD_LOGIC_VECTOR ;
               R5 : out STD_LOGIC_VECTOR ;
               R6 : out STD_LOGIC_VECTOR ;
               R7 : out STD_LOGIC_VECTOR ;
               R0 : out STD_LOGIC_VECTOR );
    end component;
    signal D,R1,R2,R3,R4,R5,R6,R7,R0 : std_logic_vector(3 downto 0);
    signal I : STD_LOGIC_VECTOR (2 downto 0);
    signal Clr, Clk : STD_LOGIC;
begin
    UUT : Register_Bank 
    port map (
       D => D ,
       I => I ,
       Clr => Clr,
       Clk => Clk,
       R1 => R1,
       R2 => R2,
       R3 => R3,
       R4 => R4,
       R5 => R5,
       R6 => R6,
       R7 => R7,
       R0 => R0
    );
    process
    begin 
        Clk <= '0';
        wait for 20ns;
        Clk <= '1';
        wait for 20ns;
    end process;
    process
    begin
        Clr <= '1';
        wait for 10ns;
        wait for 100ns;
        Clr <= '0';
        D <= "0001";
        I <= "001";
        wait for 100ns;
        D <= "0101";
        I <= "010";
        wait for 100ns;
        D <= "1100";
        I <= "111";
        wait for 100ns;
        D <= "1111";
        I <= "000";
        wait for 100 ns;
        Clr <= '1';
        wait;
         
     end process;

end Behavioral;
