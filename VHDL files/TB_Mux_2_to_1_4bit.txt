----------------------------------------------------------------------------------
-- Company: 
-- Engineer: 
-- 
-- Create Date: 19.05.2023 15:55:19
-- Design Name: 
-- Module Name: TB_Mux_2_to_1_4bit - Behavioral
-- Project Name: 
-- Target Devices: 
-- Tool Versions: 
-- Description: 
-- 
-- Dependencies: 
-- 
-- Revision:
-- Revision 0.01 - File Created
-- Additional Comments:
-- 
----------------------------------------------------------------------------------


library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

-- Uncomment the following library declaration if using
-- arithmetic functions with Signed or Unsigned values
--use IEEE.NUMERIC_STD.ALL;

-- Uncomment the following library declaration if instantiating
-- any Xilinx leaf cells in this code.
--library UNISIM;
--use UNISIM.VComponents.all;

entity TB_Mux_2_to_1_4bit is
--  Port ( );
end TB_Mux_2_to_1_4bit;

architecture Behavioral of TB_Mux_2_to_1_4bit is
    component Mux_2_to_1_4bit is
        Port (  A : in std_logic_vector;
                B : in std_logic_vector;
                S : in std_logic;
                Q : out std_logic_vector);
    end component;
    signal A,B,Q : std_logic_vector(3 downto 0);
    signal C : std_logic;

begin
    uut : Mux_2_to_1_4bit port map(
        A => A,
        B => B,
        S => C,
        Q => Q);
    process
    begin
        C <= '0';
        A <= "0000";
        B <= "0000";
        wait for 100ns;
        C <= '1';
        wait for 100ns;
        A <= "0010";
        B <= "0011";
        wait for 100ns;
        C <= '0';
        wait for 100ns;
        A <= "0100";
        B <= "0101";
        wait for 100ns;
        C <= '1';
        wait for 100ns;
        A <= "0110";
        B <= "0111";
        wait for 100ns;
        C <= '0';
        wait for 100ns;
        A <= "1000";
        B <= "1001";
        wait for 100ns;
        C <= '0';
        wait;
    end process;
end Behavioral;