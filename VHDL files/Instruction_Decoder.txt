library IEEE;
use IEEE.STD_LOGIC_1164.ALL;


entity Instruction_Decoder is
    Port ( Inst : in STD_LOGIC_VECTOR (11 downto 0);
--           Clk : in STD_LOGIC;
           Reg : in STD_LOGIC_VECTOR (3 downto 0);
           LSB : out STD_LOGIC_VECTOR (3 downto 0);
           Reg_EN : out STD_LOGIC_VECTOR (2 downto 0);
           Mux_A : out STD_LOGIC_VECTOR (2 downto 0);
           LD : out STD_LOGIC;
           Mux_B : out STD_LOGIC_VECTOR (2 downto 0);
           Sub : out STD_LOGIC;
           JMP : out STD_LOGIC);
end Instruction_Decoder;

architecture Behavioral of Instruction_Decoder is
    component D_FF
        port(
            D : in std_logic;
            Res : in std_logic;
            Clk : in std_logic;
            Q : out std_logic;
            Qbar : out std_logic);
    end component;
    signal sig_move, sig_and, sig_neg, sig_jump : std_logic;
    signal sig_move2, sig_and2, sig_neg2, sig_jump2 : std_logic_vector (2 downto 0);
    signal sig_move3, sig_and3, sig_neg3, sig_jump3 : std_logic_vector( 3 downto 0);
    signal m_LSB, a_LSB, n_LSB, j_LSB, LSB0 : std_logic_vector(3 downto 0);
    signal m_Reg_EN, a_Reg_EN, n_Reg_EN, j_Reg_EN, Reg_EN0 : std_logic_vector (2 downto 0);
    signal m_Mux_A, a_Mux_A, n_Mux_A, j_Mux_A, Mux_A0 : std_logic_vector (2 downto 0);
    signal m_LD, a_LD, n_LD, j_LD, LD0 : std_logic;
    signal m_Mux_B, a_Mux_B, n_Mux_B, j_Mux_B, Mux_B0 : std_logic_vector ( 2 downto 0);
    signal m_Sub, a_Sub, n_Sub, j_Sub, Sub0 : std_logic;
    signal m_JMP, a_JMP, n_JMP, j_JMP, JMP0 : std_logic;
    signal Res : std_logic;

begin

            
    sig_move <= (NOT Inst(10)) AND (Inst(11));
    sig_and <= (NOT Inst(10)) AND (NOT Inst(11));
    sig_neg <= (Inst(10)) AND (NOT Inst(11));
    sig_jump <= (Inst(10)) AND (Inst(11));
    
    sig_move2(0) <= sig_move; sig_move2(1) <= sig_move; sig_move2(2) <= sig_move;
    sig_and2(0) <= sig_and; sig_and2(1) <= sig_and; sig_and2(2) <= sig_and;
    sig_neg2(0) <= sig_neg; sig_neg2(1) <= sig_neg; sig_neg2(2) <= sig_neg;
    sig_jump2(0) <= sig_jump; sig_jump2(1) <= sig_jump; sig_jump2(2) <= sig_jump;
    sig_move3(0) <= sig_move; sig_move3(1) <= sig_move; sig_move3(2) <= sig_move; sig_move3(3) <= sig_move;
    sig_and3(0) <= sig_and; sig_and3(1) <= sig_and; sig_and3(2) <= sig_and; sig_and3(3) <= sig_and;
    sig_neg3(0) <= sig_neg; sig_neg3(1) <= sig_neg; sig_neg3(2) <= sig_neg; sig_neg3(3) <= sig_neg;
    sig_jump3(0) <= sig_jump; sig_jump3(1) <= sig_jump; sig_jump3(2) <= sig_jump; sig_jump3(3) <= sig_jump;
    
    --move instruction
    m_LSB <= Inst(3 downto 0);
    m_Reg_EN <= Inst(9 downto 7);
    m_Mux_A <= "000";
    m_LD <= '1';
    m_Mux_B <= "000";
    m_Sub <= '0';
    m_JMP <= '0';
    
    --add instruction
    a_LSB <= "0000";
    a_Reg_EN <= Inst(9 downto 7);
    a_Mux_A <= Inst(9 downto 7);
    a_LD <= '0';
    a_Mux_B <= Inst(6 downto 4);
    a_Sub <= '0';
    a_JMP <= '0';
    
    --neg instruction
    n_LSB <= "0000";
    n_Reg_EN <= Inst(9 downto 7);
    n_Mux_A <= "000";
    n_LD <= '0';
    n_Mux_B <= Inst(9 downto 7);
    n_Sub <= '1';
    n_JMP <= '0';
    
    --jump instruction
    j_LSB <= Inst(3 downto 0);
    j_Reg_EN <= "000";
    j_Mux_A <= Inst(9 downto 7);
    j_LD <= '1';
    j_Mux_B <= "000";
    j_Sub <= '0';
    j_JMP <= (NOT Reg(0)) AND (NOT Reg(1)) AND (NOT Reg(2)) AND (NOT Reg(3));
    
    
    
    LSB <= (m_LSB AND sig_move3) OR (a_LSB AND sig_and3) OR (n_LSB AND sig_neg3) OR (j_LSB AND sig_jump3);
    Reg_EN <= (m_Reg_EN AND sig_move2) OR (a_Reg_EN AND sig_and2) OR (n_Reg_EN AND sig_neg2) OR (j_Reg_EN AND sig_jump2);
    Mux_A <= (m_Mux_A AND sig_move2) OR (a_Mux_A AND sig_and2) OR (n_Mux_A AND sig_neg2) OR (j_Mux_A AND sig_jump2);
    LD <= (m_LD AND sig_move) OR (a_LD AND sig_and) OR (n_LD AND sig_neg) OR (j_LD AND sig_jump);
    Mux_B <= (m_Mux_B AND sig_move2) OR (a_Mux_B AND sig_and2) OR (n_Mux_B AND sig_neg2) OR (j_Mux_B AND sig_jump2);
    Sub <= (m_Sub AND sig_move) OR (a_Sub AND sig_and) OR (n_Sub AND sig_neg) OR (j_Sub AND sig_jump);
    JMP <= (m_JMP AND sig_move) OR (a_JMP AND sig_and) OR (n_JMP AND sig_neg) OR (j_JMP AND sig_jump);
end Behavioral;
