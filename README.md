# 3Wings

1- Visão Geral do Site

![image](https://user-images.githubusercontent.com/98840067/223596112-0e15efbb-b548-4c44-8568-c457b04944d8.png)
Página inicial do site da clínica médica



![image](https://user-images.githubusercontent.com/98840067/223596214-eace579b-65c0-427b-a6a7-61f8ccd6aa1b.png)
Formulário de preenchimento para marcação de consultas



![image](https://user-images.githubusercontent.com/98840067/223596306-7b2123ef-14bf-4177-8e46-fa24ff7f7abb.png)
Aba com todas as consultas marcadas para o paciente visualizar e/ou cancelar a mesma caso queira



2- Código

![preenchimento](https://user-images.githubusercontent.com/98840067/223597567-ee1563bc-1967-4b31-95d2-11f488104902.gif)
Em ConsultaForm.vue tem-se todo o formulário para o paciente preencher, nele utilizamos JSON como banco para fazer a ligação e extrair os dados, no exemplo acima vemos também uma notificação informando ao paciente que a sua consulta foi marcada com sucesso.



![preenchimento e cancelamento](https://user-images.githubusercontent.com/98840067/223598591-83b17e1b-133a-4eb7-af41-b4122d3ad937.gif)
Em Dashboard.vue tem-se todas as consultas já marcadas em que o paciente pode visualizar e cancelar, vemos novamente uma notificação informando ao mesmo que a sua consulta foi desmarcada.



Detalhe: Ao marcarmos uma consulta, os dados vão para o banco JSON e ao desmarcarmos a consulta é deletada do banco, segue imagens abaixo

![image](https://user-images.githubusercontent.com/98840067/223598406-2155e9dc-aef5-45bf-bd00-e724ffb97eee.png)

JSON com uma consulta marcada



![image](https://user-images.githubusercontent.com/98840067/223598497-dff383c4-14a3-4a8d-8af4-0e4f7fcdf07f.png)

JSON após o paciente cancelar todas as consultas
