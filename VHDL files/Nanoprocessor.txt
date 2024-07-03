library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;

entity Nanoprocessor is
    Port ( Clr : in STD_LOGIC;
           Clk : in STD_LOGIC;
           R : out STD_LOGIC_VECTOR (3 downto 0);
           Overflow : out STD_LOGIC;
           Zero : out STD_LOGIC;
           Seven_Seg : out std_logic_vector (6 downto 0));
end Nanoprocessor;

architecture Behavioral of Nanoprocessor is
    component Slow_Clk is 
        Port (  Clk_in : in std_logic;
                Clk_out : out std_logic);
    end component;
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
    component Register_Bank is
        Port ( D : in STD_LOGIC_VECTOR (3 downto 0);
               Clk : in STD_LOGIC;
               I : in STD_LOGIC_VECTOR (2 downto 0);
               Clr : in STD_LOGIC;
               R1 : out STD_LOGIC_VECTOR (3 downto 0);
               R2 : out STD_LOGIC_VECTOR (3 downto 0);
               R3 : out STD_LOGIC_VECTOR (3 downto 0);
               R4 : out STD_LOGIC_VECTOR (3 downto 0);
               R5 : out STD_LOGIC_VECTOR (3 downto 0);
               R6 : out STD_LOGIC_VECTOR (3 downto 0);
               R7 : out STD_LOGIC_VECTOR (3 downto 0);
               R0 : out STD_LOGIC_VECTOR (3 downto 0));
    end component;
    component Instruction_Decoder is
        Port ( Inst : in STD_LOGIC_VECTOR (11 downto 0);
               Reg : in STD_LOGIC_VECTOR (3 downto 0);
               LSB : out STD_LOGIC_VECTOR (3 downto 0);
               Reg_EN : out STD_LOGIC_VECTOR (2 downto 0);
               Mux_A : out STD_LOGIC_VECTOR (2 downto 0);
               LD : out STD_LOGIC;
               Mux_B : out STD_LOGIC_VECTOR (2 downto 0);
               Sub : out STD_LOGIC;
               JMP : out STD_LOGIC);
    end component;
    component Mux_2_to_1_4bit is
        Port ( A : in STD_LOGIC_VECTOR (3 downto 0);
               B : in STD_LOGIC_VECTOR (3 downto 0);
               S : in STD_LOGIC;
               Q : out STD_LOGIC_VECTOR (3 downto 0));
    end component;
    component Mux_2_to_1_3bit is
        Port ( A : in STD_LOGIC_VECTOR (2 downto 0);
               B : in STD_LOGIC_VECTOR (2 downto 0);
               S : in STD_LOGIC;
               Q : out STD_LOGIC_VECTOR (2 downto 0));
    end component;
    component ROM is
        Port ( S : in STD_LOGIC_VECTOR (2 downto 0);
               Q : out STD_LOGIC_VECTOR (11 downto 0));
    end component;
    component Program_Counter is 
         Port ( D : in STD_LOGIC_VECTOR (2 downto 0);
                Clr : in STD_LOGIC;
                Clk : in STD_LOGIC;
                Q : out STD_LOGIC_VECTOR (2 downto 0));
    end component;
    component Adder_3bit is
        Port (  A : in STD_LOGIC_VECTOR (2 downto 0); 
                S : out STD_LOGIC_VECTOR(2 downto 0);
                carry : out STD_LOGIC); 
    end component;
    component Add_Sub_4bit is
        Port ( A : in STD_LOGIC_VECTOR (3 downto 0); 
               B : in STD_LOGIC_VECTOR (3 downto 0); 
               S : out STD_LOGIC_VECTOR (3 downto 0);
               M : in STD_LOGIC;
               overflow : out STD_LOGIC);
    end component;
    
    component LUT_16_7 is
            Port ( address : in STD_LOGIC_VECTOR (3 downto 0);
                    data : out STD_LOGIC_VECTOR (6 downto 0));
    end component;
    signal PC_ROM, Add3_MuxC, PC_MuxC : std_logic_vector(2 downto 0);
    signal ROM_Decoder : std_logic_vector(11 downto 0);
    signal Decoder_MuxD : std_logic_vector(3 downto 0);
    signal Decoder_MuxC, Decoder_MuxDSelc, Decoder_Adder : std_logic;
    signal Decoder_RegBank, Decoder_MuxA, Decoder_MuxB : std_logic_vector(2 downto 0);
    signal MuxD_Adder, MuxD_RegBank : std_logic_vector(3 downto 0);
    signal R0,R1,R2,R3,R4,R5,R6,R7 : std_logic_vector(3 downto 0);
    signal MuxA_Adder, MuxB_Adder : std_logic_vector(3 downto 0);
    signal Slw_Clk : std_logic;
    signal Adder_Cout : std_logic;
    
begin
    LUT : LUT_16_7
        Port map(
            address => R7,
            data => Seven_Seg);
            
    Slow_Clk_0 : Slow_Clk
        Port map(
            Clk_in => Clk,
            Clk_out => Slw_Clk);

    Adder : Add_Sub_4bit
        Port map(
            A => MuxA_Adder,
            B => MuxB_Adder,
            M => Decoder_Adder,
            overflow => overflow,
            S => MuxD_Adder);
    MuxA : Mux_8_to_1_4bit
        Port map (
            R0 => R0,
            R1 => R1,
            R2 => R2,
            R3 => R3,
            R4 => R4, 
            R5 => R5,
            R6 => R6,
            R7 => R7,
            S => Decoder_MuxA,
            Q => MuxA_Adder);
    MuxB : Mux_8_to_1_4bit
        Port map (
            R0 => R0,
            R1 => R1,
            R2 => R2,
            R3 => R3,
            R4 => R4, 
            R5 => R5,
            R6 => R6,
            R7 => R7,
            S => Decoder_MuxB,
            Q => MuxB_Adder);
    Register_Bank_0 : Register_Bank
        Port map (
            D => MuxD_RegBank,
            Clk => Slw_Clk,
            I => Decoder_RegBank,
            Clr => Clr,
            R0 => R0,
            R1 => R1,
            R2 => R2,
            R3 => R3,
            R4 => R4, 
            R5 => R5,
            R6 => R6,
            R7 => R7);
    MuxC : Mux_2_to_1_3bit
        Port map (
            A => Add3_MuxC,
            B => Decoder_MuxD(2 downto 0),
            S => Decoder_MuxC,
            Q => PC_MuxC);
    Adder_3bit_0 : Adder_3bit
        Port map (
            A => PC_ROM,
            Carry => Adder_Cout,
            S => Add3_MuxC);
    Instruction_Decoder_0 : Instruction_Decoder
        Port map (
            Inst => ROM_Decoder,
            Reg => MuxA_Adder,
            LSB => Decoder_MuxD,
            Reg_EN => Decoder_RegBank,
            Mux_A => Decoder_MuxA,
            Mux_B => Decoder_MuxB,
            LD => Decoder_MuxDSelc,
            Sub => Decoder_Adder,
            JMP => Decoder_MuxC);
    MuxD : Mux_2_to_1_4bit
        Port map (
            A => MuxD_Adder,
            B => Decoder_MuxD,
            S => Decoder_MuxDSelc,
            Q => MuxD_RegBank);
    Program_Counter_0 : Program_Counter
        Port map ( 
            D => PC_MuxC,
            Clr => Clr,
            Clk => Slw_Clk,
            Q => PC_ROM);
    ROM_0 : ROM
        Port map (
            S => PC_ROM,
            Q => ROM_Decoder);
    R <= R7;
    Zero <= (NOT MuxD_Adder(0)) AND (NOT MuxD_Adder(1)) AND (NOT MuxD_Adder(2)) AND (NOT MuxD_Adder(3));
end Behavioral;
