library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;

entity FIFO_simple is
    Generic (
           constant ADDWIDTH  : natural := 8;  
           constant DATAWIDTH  : natural := 8
           );
    Port ( Din   		: in  STD_LOGIC_VECTOR (DATAWIDTH-1 downto 0);
           Wr_enable    : in  STD_LOGIC;
           Dout  		: out STD_LOGIC_VECTOR (DATAWIDTH-1 downto 0);
           Rd_enable   	: in  STD_LOGIC;
           Empty 		: out STD_LOGIC;
           Full  		: out STD_LOGIC;
		   Reset		: in  STD_LOGIC;
           CLK   		: in  STD_LOGIC
           );
end FIFO_simple;

architecture behavioural of FIFO_simple is

signal wrcnt : integer range 0 to ADDWIDTH-1:= 0;
signal rdcnt : integer range 0 to ADDWIDTH-1:= 0;
type memory_array is array(0 to ADDWIDTH-1) of STD_LOGIC_VECTOR (DATAWIDTH-1 downto 0);
signal memory : memory_array:= (others => (others => '0'));   
signal full_loc  : std_logic:='0';
signal empty_loc : std_logic:='1';

begin
  FIFo_process: process(CLK)
  begin
	 IF rising_edge(CLK) THEN
		if Reset='1'then
		  rdcnt<= 0;
		  wrcnt<= 0;
		  --full_loc<= '0';
		  --empty_loc<= '1';
		else
		      if (Wr_enable='1' and full_loc='0') then
				memory(wrcnt) <= Din;
				if wrcnt=ADDWIDTH-1 then
				wrcnt<=0;
				else
				wrcnt <= wrcnt+1;
				end if;
			 end if;
		      if (Rd_enable='1' and empty_loc='0')then
				Dout <= memory(rdcnt); 
				if rdcnt=ADDWIDTH-1 then
				rdcnt<=0;
				else
				rdcnt <= rdcnt+1;
				end if;
			end if;	
			 
		end if;
	 end if;
	 -- checking git
  end process FIFo_process;
  full_loc  <= '1' when rdcnt = wrcnt+1 else '0';
  empty_loc <= '1' when rdcnt = wrcnt   else '0';
  Full  <= full_loc;
  Empty <= empty_loc;
 end behavioural;
