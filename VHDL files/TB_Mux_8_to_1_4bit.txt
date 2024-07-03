library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.Numeric_std.all;

entity TB_Mux_8_to_1_4bit is
--  Port ( );
end TB_Mux_8_to_1_4bit;

architecture Behavioral of TB_Mux_8_to_1_4bit is
    component Mux_8_to_1_4bit is
        Port ( S : in STD_LOGIC_VECTOR;
               R0 : in STD_LOGIC_VECTOR;
               R1 : in STD_LOGIC_VECTOR;
               R2 : in STD_LOGIC_VECTOR;
               R3 : in STD_LOGIC_VECTOR;
               R4 : in STD_LOGIC_VECTOR;
               R5 : in STD_LOGIC_VECTOR;
               R6 : in STD_LOGIC_VECTOR;
               R7 : in STD_LOGIC_VECTOR;
               Q : out STD_LOGIC_VECTOR);
    end component;
    signal S : std_logic_vector(2 downto 0);
    signal Q,R0,R1,R2,R3,R4,R5,R6,R7 : std_logic_vector (3 downto 0);

begin
    uut: Mux_8_to_1_4bit port map(
        S => S,
        R0 => R0,
        R1 => R1,
        R2 => R2,
        R3 => R3,
        R4 => R4,
        R5 => R5,
        R6 => R6,
        R7 => R7,
        Q => Q);
    process
    begin
        R0 <= "0000";
        R1 <= "0001";
        R2 <= "0010";
        R3 <= "0011";
        R4 <= "0100";
        R5 <= "0101";
        R6 <= "0110";
        R7 <= "0111";
        for i in 0 to 8 loop
            S <= std_logic_vector(to_unsigned(i,3));
            wait for 100ns;
        end loop;
        wait;
    end process;
end Behavioral;
