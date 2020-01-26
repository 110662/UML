
# plantUML 

* reference

https://plantuml.com/ja/class-diagram

---
### Class 
```plantuml
@startuml

note right of api : Interface.
api "1"---"1" driver 
driver "1"---"1" mngr 
api "1"---"1" mngr 
mngr "1" o--"0..*" mbuf 
mbuf  <|-- EXTINY 
mbuf  <|-- LARGE 
api : SODA_Init()
api : SODA_Uninit()
api : SODA_Exec()
api : SODA_EndConfirm()
api : SODA_Config()
api : outnum 
api : setnum 
api : getnum 
note top of driver : drive SODA and mabic, TSUMXD.
driver : struct hdrinfo
driver : struct conf 
driver : set_param() 
note bottom of mngr : manage mbuf list.
mngr : i_nextpkt
mngr : o_nextpkt 
mngr : o_pkt
mngr : create_mblist()
mngr : trim_mblist()
mbuf : mbuf_get()
@enduml
```

```plantuml
@startuml
interface Class01
Class01 "1" *-- "many" Class02 : contains

Class03 o-- Class04 : aggregation

Class05 --> "1" Class06
@enduml
```


---
### Sequence
```plantuml
@startuml
title test 
Alice->Bob
Bob->Alice
@enduml
```
---
### Fllow Chart 

```plantuml
@startuml
title SODA_EndConfirm
start
:eventWait;
:mabic_cnt取得;
:pmb_top=pmb_next_top;
:pmb_p=pmb_next_top;
if (mabic_cnt==MAX) then(yes)
    :process;
    :SODA_Packetizeと同様の処理;
else if(mabic_cnt<MAX) then(yes)
    repeat
     :mabic_cntのpmb_pまで移動;
    repeat while (pkt_cnt<=mabic_cnt)
    :pmb_next_top=pmb_p->mb_next;
    :pmb_p->mb_next=NULL;
    :pmb_p=pmb_top;
else
    :error;
endif
:割り込み解除;
:return pmb_p;
end
@enduml
```