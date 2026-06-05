

# EXPERIMENT NO. 8

# SIMULATION AND IMPLEMENTATION OF RIPPLE COUNTER

### Submitted By

**Tharun T**
B.E. Electronics and Communication Engineering (ECE)
Saveetha Engineering College, Chennai

### Course

**EC1801 – Digital Logic Circuits Design Laboratory**

---

## AIM

To design, simulate and verify a 4-bit Ripple Counter using VHDL. This experiment corresponds to the Ripple Counter simulation experiment in the laboratory manual. 

---

## SOFTWARE REQUIRED

1. Xilinx Vivado / Xilinx ISE
2. ModelSim
3. GHDL Simulator

---

# THEORY

A Ripple Counter is an asynchronous counter in which the output of one flip-flop acts as the clock input for the next flip-flop. Since the clock signal propagates through the flip-flops one after another, a delay occurs, producing a ripple effect.

In a 4-bit Ripple Counter, four flip-flops are connected in cascade. The counter counts from 0000 to 1111 (0 to 15) and then repeats the sequence. The counter output changes asynchronously because each flip-flop is triggered by the output of the preceding flip-flop. 

---

# VHDL PROGRAM

## 4-BIT RIPPLE COUNTER

```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity ripple_counter is
    Port (
        CLK   : in STD_LOGIC;
        RESET : in STD_LOGIC;
        Q     : out STD_LOGIC_VECTOR(3 downto 0)
    );
end ripple_counter;

architecture Behavioral of ripple_counter is

signal temp : STD_LOGIC_VECTOR(3 downto 0) := "0000";

begin

process(CLK, RESET)
begin
    if RESET = '1' then
        temp <= "0000";

    elsif rising_edge(CLK) then
        temp(0) <= not temp(0);
    end if;
end process;

process(temp(0), RESET)
begin
    if RESET = '1' then
        temp(1) <= '0';

    elsif rising_edge(temp(0)) then
        temp(1) <= not temp(1);
    end if;
end process;

process(temp(1), RESET)
begin
    if RESET = '1' then
        temp(2) <= '0';

    elsif rising_edge(temp(1)) then
        temp(2) <= not temp(2);
    end if;
end process;

process(temp(2), RESET)
begin
    if RESET = '1' then
        temp(3) <= '0';

    elsif rising_edge(temp(2)) then
        temp(3) <= not temp(3);
    end if;
end process;

Q <= temp;

end Behavioral;
```

---

# TEST BENCH

```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity tb_ripple_counter is
end tb_ripple_counter;

architecture Behavioral of tb_ripple_counter is

signal CLK   : STD_LOGIC := '0';
signal RESET : STD_LOGIC := '1';
signal Q     : STD_LOGIC_VECTOR(3 downto 0);

begin

UUT: entity work.ripple_counter
port map(
    CLK   => CLK,
    RESET => RESET,
    Q     => Q
);

CLK <= not CLK after 5 ns;

process
begin
    wait for 10 ns;
    RESET <= '0';

    wait for 200 ns;

    wait;
end process;

end Behavioral;
```

---

# TRUTH TABLE

| Clock Count | Q3 | Q2 | Q1 | Q0 |
| ----------- | -- | -- | -- | -- |
| 0           | 0  | 0  | 0  | 0  |
| 1           | 0  | 0  | 0  | 1  |
| 2           | 0  | 0  | 1  | 0  |
| 3           | 0  | 0  | 1  | 1  |
| 4           | 0  | 1  | 0  | 0  |
| 5           | 0  | 1  | 0  | 1  |
| 6           | 0  | 1  | 1  | 0  |
| 7           | 0  | 1  | 1  | 1  |
| 8           | 1  | 0  | 0  | 0  |
| 9           | 1  | 0  | 0  | 1  |
| 10          | 1  | 0  | 1  | 0  |
| 11          | 1  | 0  | 1  | 1  |
| 12          | 1  | 1  | 0  | 0  |
| 13          | 1  | 1  | 0  | 1  |
| 14          | 1  | 1  | 1  | 0  |
| 15          | 1  | 1  | 1  | 1  |

This counting sequence matches the Ripple Counter truth table given in the laboratory manual. 

---

# OUTPUT

The simulation waveform shows:

* Asynchronous counting operation
* Binary sequence from 0000 to 1111
* Ripple effect between successive flip-flops

*(Insert Ripple Counter waveform screenshot here)*

---

# APPLICATIONS

* Frequency Division
* Digital Clocks
* Event Counters
* Digital Measurement Systems
* Timing Circuits

---

# RESULT

Thus, the 4-bit Ripple Counter was designed using VHDL and its counting sequence was successfully verified through simulation. The Ripple Counter operation was found to be correct. 

---

# AUTHOR DETAILS

**Name:** R.K. Vageesh Ragav
**Department:** Electronics and Communication Engineering (ECE)
**College:** Saveetha Engineering College
**Course Code:** EC1801 – Digital Logic Circuits Design Laboratory
**Experiment No.:** 8

---

# REPOSITORY STRUCTURE

```text
EXP-08-Ripple-Counter/
│
├── README.md
├── ripple_counter.vhd
├── tb_ripple_counter.vhd
├── waveform.png
└── output.png
```
