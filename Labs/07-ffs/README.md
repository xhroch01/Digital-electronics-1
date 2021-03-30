## Characteristic equations and completed tables for D, JK, T flip-flops.
   
   **q** (D) n+1 = d
   
   **q** (JK) n+1 = j * |q(2) + |k * q(n)
   
   **q** (T) n+1 = t * |q(n) + |t * q(n)

| **D** | **Qn** | **Q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-- |
   | 0 | 0 | 0 | No change |
   | 0 | 1 | 0 | Change |
   | 1 | 0 | 1 | Change |
   | 1 | 1 | 1 | No change |


   | **J** | **K** | **Qn** | **Q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-: | :-- |
   | 0 | 0 | 0 | 0 | No change |
   | 0 | 0 | 1 | 1 | No change |
   | 0 | 1 | 0 | 0 | Reset |
   | 0 | 1 | 1 | 0 | Reset |
   | 1 | 0 | 0 | 1 | Set |
   | 1 | 0 | 1 | 1 | Set |
   | 1 | 1 | 0 | 1 | Invert |
   | 1 | 1 | 1 | 0 | Invert |

   | **T** | **Qn** | **Q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-- |
   | 0 | 0 | 0 | No change |
   | 0 | 1 | 1 | No change |
   | 1 | 0 | 1 | invert |
   | 1 | 1 | 0 | invert |


## D latch
``` vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

-- Uncomment the following library declaration if using
-- arithmetic functions with Signed or Unsigned values
--use IEEE.NUMERIC_STD.ALL;

-- Uncomment the following library declaration if instantiating
-- any Xilinx leaf cells in this code.
--library UNISIM;
--use UNISIM.VComponents.all;

entity tb_d_latch is
--  Port ( );
end tb_d_latch;

architecture Behavioral of tb_d_latch is

    signal s_en     : std_logic;
    signal s_arst   : std_logic;
    signal s_d      : std_logic;
    signal s_q      : std_logic;
    signal s_q_bar  : std_logic;

begin
    uut_d_latch : entity work.d_latch
    port map (
        en    => s_en,
        arst  => s_arst,
        d     => s_d,
        q     => s_q,
        q_bar => s_q_bar
    );
    
    p_reset_gen : process
        begin
            s_arst <= '0';
            wait for 53 ns;
            
            s_arst <= '1';   
            wait for 5 ns;
            
            s_arst <= '0';        
               
            wait for 108 ns;           
            s_arst <= '1';
            
            wait;
     end process p_reset_gen;
    
    p_stimulus: process
    begin
        -- Report a note at the begining of stimulus process
        report "Stimulus process started" severity note;
        s_en <= '0';
        s_d  <= '0';

        --d sequence
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        --/d sequence

        s_en <= '1';
        
        wait for 3 ns;
        assert(s_q = '0' and s_q_bar = '1')
        report "chyba" severity error;
        
        --d sequence
        wait for 7 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_en <= '0'; 
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        --/d sequence
        
        wait for 3 ns;
        assert(s_q = '1' and s_q_bar = '0')
        report "chyba" severity error;
        
        --d sequence
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        --/d sequence
        
        s_en <= '1';
        wait for 3 ns;
        assert(s_q = '1' and s_q_bar = '1')
        report "chyba" severity error;
                
        --d sequence
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        s_d <= '1';
        wait for 10 ns;
        s_d <= '0';
        wait for 10 ns;
        --/d sequence
        
        report "Stimulus process finished. " severity note;       
        wait;
     end process p_stimulus;

end Behavioral;
```
