Selenium ide ptBR
=================

Tradução da Documentação e exemplos práticos dos Comandos do Selenium  IDE - Componente do Firefox para Teste de Softwarers.

Obs.: Documentação não oficial. Tradução feita no Google T. e leituras.

Aceito colaboração: contato: malcher.malch@gmail.com

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
Um **comando** é o que dizer ao Selenium o que fazer. Comandos no Selenium vêm em três "sabores": **'Ações'**, **'Accessors'** e **'Afirmações'**. Cada chamada comando é uma linha na tabela de teste da forma:
<br>
<table>
<tr>
    <td>Command</td>
    <td>target</td>
    <td>value</td>
    
</tr>
</table>

**Ações** são comandos que geralmente manipulam o estado do aplicativo. Eles fazem coisas como "clique neste link" e "selecionar a opção". Se uma ação falhar, ou tem um erro, a execução do teste atual é interrompido.

Muitas ações podem ser chamados com o sufixo <big>"AndWait"</big>, por exemplo, <big>"ClickAndWait"</big>. Este sufixo diz Selenium que a ação fará com que o navegador para fazer uma chamada para o servidor, e que o selênio deve esperar por uma nova página para carregar.

**Accessors **examinar o estado de aplicação e armazenar os resultados de variáveis, por exemplo, "StoreTitle". Eles também são utilizados para gerar automaticamente afirmações.


**Afirmações** são como Accessors , mas verificam se o estado do aplicativo está em conformidade com o que é esperado . Exemplos incluem " certifique-se o título da página é X " e "verificar se esta opção está assinalada" .

Todas as afirmações do selenium pode ser usadas em três modos: "assert", "verify", e "waitFor". Por examplo, você pode "assertText", "verifyText" e "waitForText". Quando um "assert" falhar, o teste é abortado. Quando um "verify" falhar, o teste vai continuar a execução, registrando o fracasso. Isso permite que um único "assert" para garantir que a aplicação está na página correta, seguido por um bando de "verify" asserções para testar valores de campos de formulários, etiquetas, etc

Comandos **"waitFor"** espera por alguma condição para se tornar verdade (o que pode ser **útil para testar aplicações Ajax**). Eles irão suceder imediatamente se a condição já é verdade. No entanto, eles vão falhar e interromper o teste, se a condição não se tornar realidade dentro da definição do tempo limite de corrente (ver a ação ***setTimeout*** abaixo).

**Localizadores de elementos**(Element Locators) dizem qual elemento HTML de um comando ele se refere. Muitos comandos exigem um ***Element Locator*** como o atributo "target". Exemplos de "Elemento localizadores" incluem **"elementId"** e " document.forms[0].element" . Estes são descritos de forma mais clara na próxima seção .

Os **Padrões** são utilizados por vários motivos, por exemplo, para especificar o valor esperado de um campo de entrada , ou identificar uma opção de escolha. Selenium suporta vários tipos de padrão, incluindo - as expressões regulares, os quais são descritos mais detalhadamente abaixo.

Define um objeto que executa comandos Selenium.

Element Locators
=================

Localizador Selênio dizer qual elemento HTML de um comando se refere. O formato de um localizador é:

locatorType = argumento

Apoiamos as seguintes estratégias para localizar elementos:
- identificador = ID : Selecione o elemento com o atributo @id especificado. Se nenhuma correspondência for encontrada, selecione o primeiro elemento cujo atributo de nome @ é id. (Isto é normalmente o padrão, veja abaixo.)

 - id = ID : Selecione o elemento com o atributo @ id especificado.
- nome = nome : Selecione o primeiro elemento com o especificado @ atributo nome.
 - nome de usuário
 - name = nome de usuário

O nome pode, opcionalmente, ser seguido por um ou mais elementos-filtros , separados a partir do nome de espaço em branco. Se o FilterType não for especificado, o valor é assumido.

	nome = valor sabor de chocolate =

- dom = javascriptExpression : Encontre um elemento avaliando a cadeia especificada. Isto permite-lhe percorrer o modelo de objeto de documento HTML usando JavaScript. Note que você não deve retornar um valor nessa cadeia; simplesmente tornar a última expressão no bloco.
 - dom = document.forms ['myForm']. myDropdown
 - dom = document.images [56]
 - dom = document.links função foo () {return [1]; }; foo ();

- XPath = XpathExpression : Localize um elemento usando uma expressão XPath.
	- XPath = / / img [@ alt = 'O texto alt imagem']
	- XPath = / / table [@ id = 'tabela1'] / / tr [4] / td [2]
	- XPath = / / a [contains (@ href, '# id1')]
	- XPath = / / a [contains (@ href, '# id1')] / @ class
	- XPath = (/ / table [@ class = 'stylee']) / / th [text () = 'theHeaderText'] /.. / td
	- XPath = / / input [@ name = 'nome2' e @ value = 'yes']
	- XPath = / / * [text () = "right"]



- ligação = textpattern : Selecione o link (âncora) elemento que contém o texto correspondente a determinado padrão .
link = O texto do link

- css = cssSelectorSyntax : Selecione o elemento usando seletores CSS. Por favor, consulte seletores CSS2 , seletores CSS3 para mais informações. Você também pode verificar o teste TestCssLocators no conjunto de testes de selênio para um exemplo de uso, que está incluído no pacote de núcleo selênio baixado.
	- css = a [href = "# id3"]
	- css = vão # firstChild + extensão

Atualmente, o localizador seletor css suporta todos os seletores css1, CSS2 e CSS3, exceto namespace em CSS3, alguns pseudo classes: (nth-of-type,: nth-last-of-type,: first-of-type,: last-of- Tipo,: only-of-type,: visited,: hover,: active,: foco,: indeterminado) e pseudo elementos (:: primeira linha, :: first-letter, :: :: seleção, antes, :: depois).


- ui = uiSpecifierString : Localize um elemento por resolver a corda especificador UI para outro localizador, e avaliá-las. Veja a referência Selenium UI-Element para mais detalhes.
	- ui = loginPages :: loginButton ()
	- ui = settingsPages :: alternância (label = Esconder e-mail)
	- ui = forumPages :: postBody (index = 2) / / a [2]

Sem um prefixo localizador explícito, Selenium usa as seguintes estratégias padrão:
