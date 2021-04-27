# README

## Basics

- O arquivo CSS em que estão os estilos e tudo é o `syles2.css`, só ir nele se precisar mudar o estilo de algo.

### Front Matter

- De maneira geral, pra ficar com o layout padronizado (como todas estao) toda nova pagina deve ter a _Front Matter_ no seu inicio, que consiste basicamente em:

```
---
layout: default
title: (titulo da pag)
---

```
- Embaixo disso, pode começar a escrever **direto** na linguagem de marcaçao que for, seja HTML, Markdown ou alguma outra que o Jekyll suporte.
	+ Ainda, se for escrever em HTML, pode começar direto na tag de conteudo mesmo que voce quiser, o `default` ja abstrai aquele inicio de todo arquivo HTML pra ajudar a ficar padronizado e evitar repetir codigo mesmo. (Vide qualquer uma das paginas pra ter um exemplo).
- Esse `layout: default` so vai mudar se tiver um outro modelo de layout.
- Podem ser inseridas mais variaveis tambem. Pra mais informaçoes: <https://jekyllrb.com/docs/step-by-step/03-front-matter/>




## default.html

- Eh nesse arquivo que fica o layout padrao da pagina, mais especificamente com:
	+ `<head>`
	+ Navbar
	+ Footer
- A variavel `{{ content }}` eh o que substitui todo o conteudo de uma pagina no `default.html`, o que ta no lugar de `{{ content }}` eh o que diferencia uma pagina da outra. Alem disso, ela ta dentro de um `<div id="conteudo">`, junto com o `<footer>` porque faz parte da estruturaçao da pagina. 

### <head>

- Alem do padrao que precisa pro HTML e CSS, no head tem:
	+ Chamada do arquivo de estilo CSS.
	+ Chamada da fonte.
	+ Chamada do Bootstrap.

### Navbar

- A navbar ja eh responsive, mudando de forma pra telas medias e _mobile_.
- Dentro da navbar tem alguns codigos Liquid, que eh parte da logica do Jekyll pra estruturar a pagina. 
- Basicamente ela separa a lista de links em um outro arquivo html `navigation.html`, e usa algumas logicas pra mudar a cor do link da pagina atual.

### Footer
- O footer eh bem simples, o estilo dele ta definido mais no arquivo CSS mesmo.




