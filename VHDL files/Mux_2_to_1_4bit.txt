library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity Mux_2_to_1_4bit is
    Port ( A : in STD_LOGIC_VECTOR (3 downto 0);
           B : in STD_LOGIC_VECTOR (3 downto 0);
           S : in STD_LOGIC;
           Q : out STD_LOGIC_VECTOR (3 downto 0));
end Mux_2_to_1_4bit;

architecture Behavioral of Mux_2_to_1_4bit is

begin
    Q(0) <= (A(0) AND (NOT S)) OR (B(0) AND S);
    Q(1) <= (A(1) AND (NOT S)) OR (B(1) AND S);
    Q(2) <= (A(2) AND (NOT S)) OR (B(2) AND S);
    Q(3) <= (A(3) AND (NOT S)) OR (B(3) AND S);
end Behavioral;
