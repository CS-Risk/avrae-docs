# MIMsy the Mirror Image Manager
*By Derixyleth#0636.*

MIMsy is a *mirror image* manager. MIMsy casts *mirror image* and sets a cvar for you active duplicates. Then, whenever you're attacked, run `!mim check <attack roll> [damage roll]` and MIMsy will check if the attack targeted a duplicate or your character. If the attack targeted a duplicate, it will adjust your HP up by [damage roll]. `!mim` with no args will give you more details.


### Code
```
!alias mim {{s,c,a,n="&1&",combat(),"&*&".lower().split(" "),name}}{{m=4 if s in "cast" else 3 if s in "check" else 2 if s in "drop" else 1 if s in "help&1&" else 0}}{{G=get_slots(int(a[a.index("-l")+1]) if a.count("-l") else 2)}}{{set_cvar("dupes",3) if m==4 and G else set_cvar("dupes",0) if m==2 else set_cvar_nx("dupes",0)}}{{du,k,d,r=int(dupes),int("&2&") if "&2&".isdigit() else 0,int("&3&") if "&3&".isdigit() else 0,vroll("1d20")}}{{RO,DAC=12-du-(du if du>1 else 0),10+dexterityMod}}{{t,DN=(r.total>=RO),[n,"a duplicate"]}}{{h,HM=k>=DAC if t else k>armor,["missed","hit"]}}{{set_hp(min(hp,d+get_hp())) if t and m==3 else ""}}{{mT=load_json(get_gvar("f2398218-0cce-4834-904e-2983675b9600").replace("HM",HM[h]).replace("DN",DN[t]).replace("NU",str(du)).replace("S ","s " if du>1 else " ").replace("RO",str(RO)).replace("DAC",str(DAC)).replace("NA",n))}}{{nu=max(0,(du-(h and t))) if m==3 else du}}{{'i ' if c and m==4 else ''}}{{mT.C+('&*&'.replace('&1& ','')) if m>3 else mT.M+' -f "d20 Roll|'+str(r)+'" -f "Duplicates|'+('◉'*nu + '〇'*(3-nu))+('" -f "'+n+'\'s Adjusted HP|'+str(get_hp())+'/'+str(hp) if t and d else '')+'"' if m>2 and du else mT.D if m==2 else mT.H if m==1 else mT.N}}{{mT.F}}{{set_cvar("dupes",nu)}}{{c.me.remove_effect("Mirror Image") if c and ((m==3 and not nu) or m==2) else ''}} -color <color> -image <thumb>
```
