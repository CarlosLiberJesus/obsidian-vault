# Week Tasks Aggregate

>[!summary]
> # Domingo, `$= dv.date("today").minus({ days: dv.date("today").weekday % 7 }).toFormat("MMM dd")` 
>
> > [!tarefas]
> >```tasks
> >not done
> >(due on this sunday) OR ((scheduled in or before this sunday) AND (due in or after this sunday))
> >hide due date
> >sort by priority
> >```
> 

> [!summary]
> # Segunda, `$= dv.date("today").minus({ days: dv.date("today").weekday % 7 }).plus({ days: 1 }).toFormat("MMM dd")`
> > [!tarefas]
> >```tasks
> >not done
> >(due on this monday) OR ((scheduled in or before this monday) AND (due in or after this monday))
> >hide due date
> >sort by priority
> >```
> 

> [!summary]
> # Terça, `$= dv.date("today").minus({ days: dv.date("today").weekday % 7 }).plus({ days: 2 }).toFormat("MMM dd")`
> > [!tarefas]
> >```tasks
> >not done
> >(due on this tuesday) OR ((scheduled in or before this tuesday) AND (due in or after this tuesday))
> >hide due date
> >sort by priority
> >```
> 

> [!summary]
># Quarta, `$= dv.date("today").minus({ days: dv.date("today").weekday % 7 }).plus({ days: 3 }).toFormat("MMM dd")`
> > [!tarefas]
> >```tasks
> >not done
> >(due on this wednesday) OR ((scheduled in or before this wednesday) AND (due in or after this wednesday))
> >hide due date
> >sort by priority
> >```
> 


> [!summary]
># Quinta, `$= dv.date("today").minus({ days: dv.date("today").weekday % 7 }).plus({ days: 4 }).toFormat("MMM dd")`
> > [!tarefas]
> >```tasks
> >not done
> >(due on this thursday) OR ((scheduled in or before this thursday) AND (due in or after this thursday))
> >hide due date
> >sort by priority
> >```
>


> [!summary]
># Sexta, `$= dv.date("today").minus({ days: dv.date("today").weekday % 7 }).plus({ days: 5 }).toFormat("MMM dd")`
> > [!tarefas]
> > ```tasks
> >not done
> >(due on this friday) OR ((scheduled in or before this friday) AND (due in or after this friday))
> >hide due date
> >sort by priority
> >```


> [!summary]
> # Sábado, `$= dv.date("today").minus({ days: dv.date("today").weekday % 7 }).plus({ days: 6 }).toFormat("MMM dd")`
> > [!tarefas]
> ># Sábado
> >```tasks
> >not done
> >(due on this saturday) OR ((scheduled in or before this saturday) AND (due in or after this saturday))
> >hide due date
> >sort by priority
> >```
> 



# Tarefas planeadas
```tasks
not done
due after saturday
group by due
sort by priority
```

# Todas as Tarefas
```tasks
path does not include All-Checkboxs
path does not include Template
path does not include index
path does not include Tech-Stack
```

