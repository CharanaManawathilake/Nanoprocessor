library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;

entity TB_ROM is
--  Port ( );
end TB_ROM;

architecture Behavioral of TB_ROM is
    component ROM is
        Port (
            S : in std_logic_vector;
            Q : out std_logic_vector);
    end component;
    signal S : std_logic_vector(2 downto 0);
    signal Q : std_logic_vector(11 downto 0);

begin
    uut: ROM port map(
        S => S, 
        Q => Q);
    process
    begin
        for i in 0 to 5 loop
            S <= std_logic_vector(to_unsigned(i,3));
            wait for 100ns;
        end loop;
        wait;
    end process;
end Behavioral;
