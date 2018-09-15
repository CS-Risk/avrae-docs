# setrace
*By Derixyleth#0636.*

Sets your race, sets up any custom counters for that race, adds cvars for languages, resistances, size, speeds, and senses. Supports all published races and the races from Wayfinder's Guide to Eberron.

```md
!alias setrace embed {{a,B,Q,A="&*&".lower().split(" ")if"&*&"else[],'','"',"'"}}{{r,s,e=a[0] if a else B,B if '&1&' in 'dragonborn' else a[1] if len(a)>1 else B,a[2] if a and len(a)>2 else B}}{{g=load_json(get_gvar("c938f615-47ed-4ddf-bbf3-97feb9f913f9"))}}{{x=[x for x in g if 'ccs' in x and r in x.race.lower() and s in x.sub.lower() and (e in x.sub.lower() if e else 1)] if a else B}}{{x=x[0]if x else B}}{{dbt=a[1].title() if len(a)>1 else B}}{{n=(x.sub+' ' if x.sub else B)+(dbt+' ' if r in "dragonborn" else B)+x.race if 'race' in x else ((a[1]+' ' if len(a)>1 else B)+a[0]).title() if a else B}}{{n=n.replace(" Gith","").replace(" Elf"if"Shadar"in n else "","")}}{{R=x.res if x else []}}{{dr=[R.append(g[14][i]) if dbt in g[13][i] else B for i in range(5)] if len(a)>1 and r in "dragonborn" else B}}{{set_cvar("race",n) if a else B,set_cvar("dborn",a[1]) if r in "dragonborn" and len(a)>1 else B,set_cvar("langs",", ".join(x.lan) if x else "Common") if a else B,set_cvar("resists",", ".join(R) if R else B) if a else B,set_cvar("size",x.size if x else "Medium") if a else B,set_cvar("senses",x.sen if x else B) if a else B,set_cvar("speed",x.spd if x else "30 ft.") if a else B,set_cvar("immunes",x.imm if x and x.imm else B) if a else B}}{{ccc=[create_cc_nx(x.ccs[i],0,1,x.ccr[i],"bubble") if level>=x.ccl[i] else B for i in range(len(x.ccs))] if x else B}} -title "<name> {{g[3]+n+A if x else g[4]if a else g[5]}}!"{{g[11]+size+Q+g[7]+speed+Q+(g[9]+resists+Q if resists else B)+(g[10]+immunes+Q if immunes else B)+(g[12]+senses+Q if senses else B)+(g[6]+', '.join(x.ccs)+'"'if x.ccs else B)+g[8]+langs+Q if x else g[1].replace("RACE",n)if a else g[0]}}{{g[2]}} -color <color> -thumb <image>
```