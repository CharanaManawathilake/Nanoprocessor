library IEEE;
use IEEE.STD_LOGIC_1164.ALL;


entity TB_Nanoprocessor is
--  Port ( );
end TB_Nanoprocessor;

architecture Behavioral of TB_Nanoprocessor is
    component Nanoprocessor is
        Port (
            Clr : in std_logic;
            Clk : in std_logic;
            R : out std_logic_vector;
            Overflow : out std_logic;
            Zero : out std_logic;
            Seven_Seg : out std_logic_vector );
    end component;
    signal Clr, Clk, Overflow, Zero : std_logic;
    signal R : std_logic_vector( 3 downto 0);
    signal Seven_Seg : std_logic_vector (6 downto 0) ;

begin
    uut : Nanoprocessor
        port map (
            Clr => Clr,
            Clk => Clk,
            R => R,
            Overflow => Overflow,
            Zero => Zero,
            Seven_Seg => Seven_Seg);
    process
    begin
        Clk <= '0';
        wait for 5ns;
        Clk <= '1';
        wait for 5ns;
    end process;
    process
    begin
        Clr <= '1';
        wait for 20ns;
        Clr <= '0';
        wait;
    end process;


end Behavioral;
