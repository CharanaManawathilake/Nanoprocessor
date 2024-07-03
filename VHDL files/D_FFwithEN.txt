library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity D_FFwithEN is
    Port ( D : in STD_LOGIC;
           Res : in STD_LOGIC;
           Clk : in STD_LOGIC;
           Q : out STD_LOGIC;
           EN : in std_logic;
           Qbar : out STD_LOGIC);
end D_FFwithEN;

architecture Behavioral of D_FFwithEN is

begin
    process (Clk) begin
        if (rising_edge(Clk)) then
            if Res = '1' then
                Q <= '0';
                Qbar <= '1';
            else
                if EN = '1' then
                    Q <= D;
                    Qbar <= not D;
                end if;
            end if;
        end if;
    end process;
end Behavioral;