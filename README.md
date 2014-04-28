Selenium ide ptBR
=================

Tradução da Documentação dos Comdos do Selenium  IDE - Componente do Firefox para Teste de Softwarers.

Obs.: Documentação não oficial.

Documento de Referência Selenium IDE 

<ol>
<li>Conceitos</li>
    <ol>
        <li>Elemento localizadores</li> 
        <li>Elemento Filtros</li> 
        <li>Padrões String-match</li> 
    </ol>
<li>Ações do Selenium</li> 
<li>Acessórios Selenium</li> 
<li>Parâmetro Construção e Variáveis </li>
<li>Regras de espaço em branco </li>
<li>Estendendo Selenium</li>
</ol>

Conceitos
=================
Um comando é o que dizer ao Selenium o que fazer. Comandos no Selenium vêm em três "sabores": 'ações', 'alvos' e 'valor'. Cada chamada comando é uma linha na tabela de teste da forma:
<br>
<table>
<tr>
    <td>Command</td>
    <td>target</td>
    <td>value</td>
    
</tr>
</table>

Ações são comandos que geralmente manipulam o estado do aplicativo. Eles fazem coisas como "clique neste link" e "selecionar a opção". Se uma ação falhar, ou tem um erro, a execução do teste atual é interrompido.

Muitas ações podem ser chamados com o sufixo <big>"AndWait"</big>, por exemplo, <big>"ClickAndWait"</big>. Este sufixo diz Selenium que a ação fará com que o navegador para fazer uma chamada para o servidor, e que o selênio deve esperar por uma nova página para carregar.