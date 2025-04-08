# <% tp.date.now("dddd, DD [de] MMMM [de] YYYY", 0, tp.file.title, "YYYY-MM-DD") %>
[[Daily Logs/<%tp.date.now("YYYY-MM-DD", -1, tp.file.title,"YYYY-MM-DD")%>|Ontem]]  <-> [[Daily Logs/<%tp.date.now("YYYY-MM-DD", +1, tp.file.title,"YYYY-MM-DD")%>|Amanhã]]
Visão Semanal: [[Weekly Logs/<%moment(tp.file.title).format("gggg-[W]ww")%>| Semana <%moment(tp.file.title).format("W")%>]]


> [!atraso]
> ```tasks
> not done
> due before {{date:YYYY-MM-DD}}
> sort by priority
> ```

> [!tarefas]
>```tasks
>not done
>(due on {{date:YYYY-MM-DD}}) OR ((scheduled in or before {{date:YYYY-MM-DD}}) AND (due in or after {{date:YYYY-MM-DD}}))
>hide due date
>sort by priority
>```

> [!summary]
> ```tasks
> done on {{date:YYYY-MM-DD}}
> ```


## Objectivos



## Notas



## Tarefas QuickAdd




> [!amanha]
> 
> ## 💼 Tarefas
>
>```tasks
>not done
>(due on {{date+1d:YYYY-MM-DD}}) OR ((scheduled in or before {{date+1d:YYYY-MM-DD}}) AND (due in or after {{date+1d:YYYY-MM-DD}}))
>hide due date
>sort by priority
>```

