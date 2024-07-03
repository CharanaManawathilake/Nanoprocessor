library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;


entity ROM is
    Port ( S : in STD_LOGIC_VECTOR (2 downto 0);
           Q : out STD_LOGIC_VECTOR (11 downto 0));
end ROM;

architecture Behavioral of ROM is
    type rom_type is array (0 to 7) of std_logic_vector(11 downto 0);
        signal ROM  : rom_type := (
-------------- Countdown from 7 to 1.---------------------------
--            "100010000111", -- MOVI R1, 111
--            "100100000001", -- MOVI R2, 1
--            "010100000000", -- NEG R2
--            "000010100000", -- ADD R1, R2
--            "110010000111", -- JZR R1, 7
--            "111110000011", -- JZR R0, 3
--            "110000000111", -- JZR R0, 7
--            "110000000111"  -- JZR R0, 7
--            );

--------------- Add numbers from 3 to 1-----------------------------
              "100010000011", -- MOVI R1, 3
              "100100000001", -- MOVI R2, 1
              "010100000000", -- NEG R2
              "001110010000", -- ADD R7, R1   
              "000010100000", -- ADD R1, R2
              "110010000111", -- JZR R1, 7
              "110000000011", -- JZR R0, 3
              "110000000111"  -- JZR R0, 7
              );
begin
    Q <= ROM(to_integer(unsigned(S)));
end Behavioral;
