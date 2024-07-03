library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity Register_4bit is
    Port ( Clk : in STD_LOGIC;
           Val : in STD_LOGIC_VECTOR (3 downto 0);
           Sel : in STD_LOGIC;
           Clr : in STD_LOGIC;
           Reg_out : out STD_LOGIC_VECTOR (3 downto 0));
end Register_4bit;

architecture Behavioral of Register_4bit is
    component D_FFwithEN
        port(
            D : in std_logic;
            Res : in std_logic;
            Clk : in std_logic;
            Q : out std_logic;
            EN : in std_logic;
            Qbar : out std_logic);
    end component;
    signal Activate : std_logic;

begin
    D_FF_0 : D_FFwithEN
        port map(
            D => Val(0),
            Res => Clr,
            Clk => Clk,
            EN => Sel,
            Q => Reg_out(0));
    D_FF_1 : D_FFwithEN
        port map(
            D => Val(1),
            Res => Clr,
            Clk =>  Clk,
            EN => Sel,
            Q => Reg_out(1));
    D_FF_2 : D_FFwithEN
        port map(
            D => Val(2),
            Res => Clr,
            Clk =>  Clk,
            EN => Sel,
            Q => Reg_out(2));
    D_FF_3 : D_FFwithEN
        port map(
            D => Val(3),
            Res => Clr,
            Clk =>  Clk,
            EN => Sel,
            Q => Reg_out(3));
end Behavioral;
