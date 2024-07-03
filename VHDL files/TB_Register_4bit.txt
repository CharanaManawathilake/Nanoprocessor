library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity TB_Register_4bit is
--  Port ( );
end TB_Register_4bit;

architecture Behavioral of TB_Register_4bit is
    component Register_4bit is 
        Port (
            Clk : in std_logic;
            Val : in std_logic_vector;
            Sel : in std_logic;
            Clr : in std_logic;
            Reg_out : out std_logic_vector);
    end component;
    signal Clk, Sel, Clr : std_logic;
    signal Val, Reg_out : std_logic_vector (3 downto 0);

begin
    uut : Register_4bit
        Port map (
            Clk => Clk,
            Val => Val,
            Sel => Sel,
            Clr => Clr,
            Reg_out => Reg_out);
    process
    begin 
        Clk <= '0';
        wait for 50ns;
        Clk <= '1';
        wait for 50ns;
    end process;
    process
    begin
        Clr <= '0';
        Sel <= '1';
        wait for 10ns;
        Val <= "1111";
        wait for 100ns;
        Val <= "1001";
        wait for 100ns;
        Val <= "1100";
        wait for 100ns;
        Sel <= '0'; 
        Val <= "1010";
        wait for 100ns;
        Sel <= '1';
        Val <= "0110";
        wait;
    end process;

end Behavioral;
