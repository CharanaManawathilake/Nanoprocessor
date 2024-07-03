library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity Program_Counter is
     Port ( D : in STD_LOGIC_VECTOR (2 downto 0);
            Clr : in STD_LOGIC;
            Clk : in STD_LOGIC;
            Q : out STD_LOGIC_VECTOR (2 downto 0));
end Program_Counter;

architecture Behavioral of Program_Counter is
    component D_FF 
        port ( 
           D : in STD_LOGIC;
           Res : in STD_LOGIC;
           Clk : in STD_LOGIC;
           Q : out STD_LOGIC);
    end component;

begin
    D_FF0 : D_FF 
        port map ( 
        D => D(0),
        Q => Q(0),
        Res =>Clr,
        Clk => Clk);
    
    D_FF1 : D_FF 
        port map ( 
        D => D(1),
        Q => Q(1),
        Res =>Clr,
        Clk => Clk);
        
    D_FF2 : D_FF 
        port map ( 
        D => D(2),
        Q => Q(2),
        Res =>Clr,
        Clk => Clk);
end Behavioral;
