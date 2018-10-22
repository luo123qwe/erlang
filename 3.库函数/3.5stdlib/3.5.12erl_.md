```erlang
1.{ok,Scanned,_} = erl_scan:string( "1+2*2+(2+4)/2." ).
    {ok,[{integer,1,1},
     {'+',1},
     {integer,1,2},
     {'*',1},
     {integer,1,2},
     {'+',1},
     {'(',1},
     {integer,1,2},
     {'+',1},
     {integer,1,4},
     {')',1},
     {'/',1},
     {integer,1,2}],
    1}
2.{ok,Parsed} = erl_parse:parse_exprs(Scanned),
  {ok,[{op,1,'+',
         {op,1,'+',
             {integer,1,1},
             {op,1,'*',{integer,1,2},{integer,1,2}}},
         {op,1,'/',
             {op,1,'+',{integer,1,2},{integer,1,4}},
             {integer,1,2}}}]}
3.erl_eval:exprs(Parsed,[]).
    {value,8.0,[]}

4.erl_syntax:abstract(T::term()) -> syntaxTree()

  {ok, T1, _} = erl_scan:string( "aaa,bbb." ).
5. erl_parse:parse_term(T1).
  T1的末尾必须是 {dot, 1}
```