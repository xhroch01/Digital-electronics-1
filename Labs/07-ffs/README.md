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
### P_D_Latch
``` vhdl
p_d_latch : process(d, arst, en)
    begin
        if (arst = '1') then
            q       <= '0';
            q_bar   <= '1';
            
        elsif (en = '1') then
            q       <= d;
            q_bar   <= not d;
            
        end if;
    end process p_d_latch;
```

### P_reset and Stimulus process

``` vhdl
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
![1](IMAGES/prubeh.PNG)

## processes p_d_ff_arst
``` vhdl
architecture Behavioral of d_ff_arst is

begin
    p_d_ff_arst : process (clk, arst)
        begin
            if (arst = '1') then
                q       <= '0';
                q_bar   <= '1';
            
            elsif rising_edge(clk) then
                q       <= d;
                q_bar   <= not d;
            
            end if;
    end process p_d_ff_arst;

end Behavioral;
```
![1](IMAGES/prubeharst.PNG)


## processes p_jk_ff_rst
``` vhdl
p_jk_ff_rst : process (clk)
        begin
            if rising_edge(clk) then
                if (rst = '1') then
                    s_q <= '0';
                    else
                        if (j = '0' and k = '0') then
                            s_q <= s_q;
                        elsif (j = '0' and k = '1') then
                            s_q <= '0';
                        elsif (j = '1' and k = '0') then
                            s_q <= '1';
                        else  (j = '1' and k = '1') then
                            s_q <= not s_q;
                        end if;
                    end if;
                end if;
    end process p_jk_ff_rst;
```


abc
``` vhdl
----------------------------------------------------------------------------------
-- Company: 
-- Engineer: 
-- 
-- Create Date: 30.03.2021 20:03:51
-- Design Name: 
-- Module Name: jk_ff_rst - Behavioral
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

entity jk_ff_rst is
Port ( 
        clk      : in  STD_LOGIC;
        rst    : in  STD_LOGIC;
        j       : in  STD_LOGIC;
        k       : in  STD_LOGIC;
        q       : out STD_LOGIC;
        q_bar   : out STD_LOGIC
        );
end jk_ff_rst;

architecture Behavioral of jk_ff_rst is
    signal s_q : std_logic;
begin
    p_jk_ff_rst : process (clk)
        begin
            if rising_edge(clk) then
                if (rst = '1') then
                    s_q <= '0';
                    else
                        if (j = '0' and k = '0') then
                            s_q <= s_q;
                        elsif (j = '0' and k = '1') then
                            s_q <= '0';
                        elsif (j = '1' and k = '0') then
                            s_q <= '1';
                        else  (j = '1' and k = '1') then
                            s_q <= not s_q;
                        end if;
                    end if;
                end if;
    end process p_jk_ff_rst;

    q <= s_q;
    q <= not s_q;

end Behavioral;
```
