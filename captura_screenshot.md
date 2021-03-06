# Captura de screenshot

Declare esta biblioteca no topo do script:
```python
import shutil
```
Abaixo temos a variávels <i>screenshotsPasta</i>, que indica o caminho da pasta a qual os arquivos de screenshot serão armazenados, e temos a função <i>numPrint_func</i>, que é um mero contador para incrementar o número da imagem a ser salva. 
```python
screenshotsPasta = "C:\Users\cciola\Desktop\Sikuli IDE\Screenshots_Sikuli\\"
```
Abaixo declaramos o valor da variável <i>numPrint</i> e em seguida declaramos a função para:
- indica que a variável <i>numPrint</i> é global
- incrementa o valor de <i>numPrint</i> em 1
```python
numPrint = 0
def numPrint_func():
    global numPrint 
    numPrint += 1
```
Esta é a função que:
- aguarda o tempo de 1 segundo para passar ao próximo passo <i>wait(1)</i>
- chama a função de incremento do número do print <i>numPrint_func</i>
- captura o screenshot <i>shutil.move(capture(Screen())</i>
- armazena o arquivo na pasta indicada no caminho informado anteriormente <i>screenshotsPasta</i>
- renomeia o arquivo conforme desejado, incrementando o valor de <i>numPrint</i> e convertendo-o para <i>string</i>, já que foi declarado como <i>int</i> na variável
- define a exrtensão do arquivo <i>.png</i>
```python
def capturaImagem_func():
    wait(1)
    numPrint_func()
    shutil.move(capture(Screen()), screenshotsPasta + 'NomeDoArquivo_' + (str(int(numPrint))) + '.png')
```

# Veja o script funcionando

Copie e cole o script abaixo no Sikuli e execute. O resultado será a exibição de um popup informando o caminho no qual o arquivo com o screenshot foi gerado.
```python
import shutil

screenshotsPasta = "C:\Users\cciola\Desktop\Sikuli_IDE\Screenshots_Sikuli\\"

#Função para incrementar 1 no número do print
numPrint = 0
def numPrint_func():
    global numPrint 
    numPrint += 1
    
#Função para capturar screenshot
def capturaImagem_func():
    wait(1)
    numPrint_func()
    shutil.move(capture(Screen()), screenshotsPasta + 'NomeDoArquivo_' + (str(int(numPrint))) + '.png')

capturaImagem_func()

popup('Script de teste finalizado com sucesso! Veja o print gerado no caminho \n %s' %screenshotsPasta)
print ('Número do arquivo gerado: %d' %numPrint)

wait(1)
exit()
```
Caso deseje capturar somente a janela que possui o foco (função similar ao Alt+PrintScreen), deve-se utilizar:
```python
firstWindow = App.focusedWindow()
firstWindow.highlight(2)
```
Aqui temos:
- o comando para verificar a janela que possui o foco <i>firstWindow = App.focusedWindow()</i>
- o comando para destacar a janela que o Sikuli está considerando como foco, indicando os segundos que o destaque será aplicado <i>firstWindow.highlight(2)</i>

Deve-se declarar a instância <i>firstwindow</i> dentro de <i>shutil.move(capture())</i>, ficando <i>shutil.move(capture(firstwindow)</i>.
Costumo declarar o trecho de código abaixo (que imprime o texto desejado no log do Sikuli) logo após a variável que efetuará o screenshot, pois caso o script dê erro ao executar e não chegue a exibir o popup, é possível verificar qual foi o último screenshot capturado.
```python
print ('Arquivo gerado: %d' %numPrint)
```
<br></br>
Dúvidas me contate! carol.ciola@gmail.com
