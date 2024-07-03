library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity TB_Program_Counter is
--  Port ( );
end TB_Program_Counter;

architecture Behavioral of TB_Program_Counter is
    component Program_Counter is
        Port (  D : in std_logic_vector;
                Clr : in std_logic;
                Clk : in std_logic;
                Q : out std_logic_vector);
    end component;
    signal D, Q : std_logic_vector (2 downto 0);
    signal Clr, Clk : std_logic;

begin
    uut: Program_Counter port map(
        D => D,
        Clk => Clk,
        Clr => Clr,
        Q => Q);
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
        wait for 10ns;
        D <= "000";
        wait for 100ns;
        D <= "001";
        wait for 100ns;
        D <= "010";
        wait for 100ns;
        D <= "011";
        wait for 50ns;
        Clr <= '1';
        wait for 50ns;
        D <= "100";
        wait for 100ns;
        D <= "101";
        wait for 100ns;
        D <= "110";
        wait for 100ns;
        D <= "111";
        wait;
    end process;
end Behavioral;
