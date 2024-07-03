library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity TB_Mux_2_to_1_3bit is
--  Port ( );
end TB_Mux_2_to_1_3bit;

architecture Behavioral of TB_Mux_2_to_1_3bit is
    component Mux_2_to_1_3bit is
        Port (  A : in std_logic_vector;
                B : in std_logic_vector;
                s : in std_logic;
                Q : out std_logic_vector);
    end component;
    signal A,B,Q : std_logic_vector(2 downto 0);
    signal C : std_logic;
    
begin
    uut : Mux_2_to_1_3bit port map(
        A => A,
        B => B,
        s => C,
        Q => Q);
    process
    begin
        C <= '0';
        A <= "000";
        B <= "000";
        wait for 200ns;
        A <= "010";
        B <= "011";
        wait for 200ns;
        C <= '1';
        wait for 200ns;
        A <= "100";
        B <= "101";
        wait for 200ns;
        C <= '0';
        wait;
    end process;
end Behavioral;
