# <%moment(tp.file.title).startOf('isoWeek').format("MMM DD")%> - <%moment(tp.file.title).endOf('isoWeek').format("MMM DD")%>
[[Weekly Logs/<%moment(tp.file.title).subtract(1,'week').format("gggg-[W]ww")%>|  <- Semana Passada]] | [[Weekly Logs/<%moment(tp.file.title).add(1,'week').format("gggg-[W]ww")%>| Para a Semana ->]]

# Dias
[[Daily Logs/<%moment(tp.file.title).startOf('isoWeek').add(0,'day').format('YYYY-MM-DD')%>|Segunda]] | [[Daily Logs/<%moment(tp.file.title).startOf('isoWeek').add(1,'day').format('YYYY-MM-DD')%>|Terça]] | [[Daily Logs/<%moment(tp.file.title).startOf('isoWeek').add(2,'day').format('YYYY-MM-DD')%>|Quarta]] | [[Daily Logs/<%moment(tp.file.title).startOf('isoWeek').add(3,'day').format('YYYY-MM-DD')%>|Quinta]] | [[Daily Logs/<%moment(tp.file.title).startOf('isoWeek').add(4,'day').format('YYYY-MM-DD')%>|Sexta]] | [[Daily Logs/<%moment(tp.file.title).startOf('isoWeek').add(5,'day').format('YYYY-MM-DD')%>|Sábado]] | [[Daily Logs/<%moment(tp.file.title).startOf('isoWeek').add(6,'day').format('YYYY-MM-DD')%>|Domingo]]


# Review Tarefas

> [!atraso]
> ```tasks
> not done
> due before {{date:YYYY-MM-DD}}
> sort by priority
> ```

> [!tarefas]
> ```tasks
> not done
> (due on or after {{date-1d:YYYY-MM-DD}} due on or before {{date+6d:YYYY-MM-DD}}) OR ((scheduled on or before {{date+6d:YYYY-MM-DD}}) AND (due on or after {{date-1d:YYYY-MM-DD}}))
> sort by priority
> ```

> [!summary]
> ```tasks
> done
> due after {{date-1d:YYYY-MM-DD}}
> due before {{date+6d:YYYY-MM-DD}}
> sort by priority
> ```
## Objectivos



## Reflexões



## Próximas Actividades
> [!para-a-semana]
> 
> ## 💼 Tarefas
> ```tasks
> not done
> (due on or after {{date+7d:YYYY-MM-DD}} due on or before {{date+13d:YYYY-MM-DD}}) OR ((scheduled on or before {{date+13d:YYYY-MM-DD}}) AND (due on or after {{date+7d:YYYY-MM-DD}}))
> hide due date
> sort by priority
>```


