library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity TB_Instruction_Decoder is
--  Port ( );
end TB_Instruction_Decoder;

architecture Behavioral of TB_Instruction_Decoder is
    component Instruction_Decoder is
        Port (  Inst : in std_logic_vector;
--                Clk : in std_logic;
                Reg : in std_logic_vector;
                LSB : out std_logic_vector;
                Reg_EN : out std_logic_vector;
                Mux_A : out std_logic_vector;
                LD : out std_logic;
                Mux_B : out std_logic_vector;
                Sub : out std_logic;
                JMP : out std_logic);
    end component;
    signal Inst : std_logic_vector (11 downto 0);
    signal LD, Sub, JMP : std_logic; 
    signal Reg, LSB : std_logic_vector (3 downto 0);
    signal Mux_A, Mux_B, Reg_EN : std_logic_vector (2 downto 0);

begin
    uut: Instruction_Decoder port map(
        Inst => Inst,
        Reg => Reg,
        LSB => LSB,
        Reg_EN => Reg_EN,
        Mux_A => Mux_A,
        LD => LD,
        Mux_B => Mux_B,
        Sub => Sub,
        JMP => JMP);

    process
    begin
        wait for 5ns;
        Reg <= "0000";
        Inst <= "100010000010";
        wait for 80ns;
        Inst <= "100100000001";
        wait for 80ns;
        Inst <= "010100000000";
        wait for 80ns;
        Inst <= "000010100000";
        wait for 80ns;
        Inst <= "110010000111";
        wait for 80ns;
        Reg <= "0100";
        wait for 80ns;
        Inst <= "111110000011";
        wait;
    end process;
end Behavioral;
