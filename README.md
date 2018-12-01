# Interpretador-de-Comandos-em-Python
Intepretador básico com algumas funcionalidades, desenvolvido em python 
Autor: João Vitor Da Silva Correia
Data: 05/07/2016


import os   #importa a Biblioteca os / para as chamadas de sistema
import shutil #importa a Biblioteca para manipular diretorios(mover,copiar)
from datetime import datetime #importa a Biblioteca datetime (que me mostra a hora, data, e etc.)
import os.path #importa o comando path da biblioteca os (para verificar os diretorios existentes)


def interpretador():
      os.system("title INTERPRETADOR DE COMANDOS ") #Modifica o nome do intepretador
      print("") #pula espaço
      sair = False   #o comando sair recebe falso
      while(sair == False):  #enquanto o sair for falso, o while executara
            op = input(">>> ") #op é a variavel que recebe o comando
            operacao = op.split(" ",3) # o split quebra a string digitada, e joga a palvra em um vetor


            #Bloco com apenas um comando de entrada
            if len(operacao) == 1:  #conta a quantidade de argumentos / se for igual a um entra no bloco
                  if(operacao[0] == "SAIR"):  #se o comando for igual a "SAIR"
                        break #quebra o while
                        exit  #sai da função
                  elif(operacao[0] == "LISTAR"): #se o comando for igual a listar  
                        print(os.system('dir')) #ele lista o diretorio atual aonde está localizado o este arquivo
                  elif(operacao[0] == "AJUDA"): # se comando for igual a ajuda
                        ajuda() #imprime a lista de comandos
                  elif(operacao[0] == "VERSÃO"): #se operacao for igual a versão 
                        os.system('winver') #chamada se sistema q imprime a versão(no Windows)
                        os.system('ver')
                  elif(operacao[0] == "DATA"): #se operacao for igual a data
                        now = datetime.now() #chamada de sistema da biblioteca datetime
                        print ("\n",now.day,"/",now.month,"/",now.year,"\n") #imprime o dia
                  elif(operacao[0] == "HORA"): #se comando for igual a hora
                        now = datetime.now() #chamada de sistema da biblioteca datetime
                        print("\n",now.hour,":",now.minute,":",now.second,"\n") #imprime a hora, minuto,segundo
                  elif(operacao[0] == "LIMPAR"): #se comando for igual a limpar
                        os.system('cls') #chamada de sistema q limpa a tela (funciona só no prompt)
                  elif(operacao[0] == "GOOGLE"): #se comando for igual a google
                        os.system('google.url') #abre o navegador

                  else: #se nenhum dos comandos for selecionado
                        print("Comando Invalido !") #exibe msg de erro
            #fim do bloco com apenas uma entrada  





            #Bloco com dois comandos de entrada 
            elif len(operacao) == 2: #conta a quantidade de argumentos / se for igual a dois entra no bloco
                 if(operacao[0] == "LISTAR"):#se comando for igual a listar
                       if(os.path.exists(operacao[1])): #verifica se o diretorio existe
                             print(os.listdir(operacao[1])) #imprime os arquivos do diretorio
                       else: #caso contrario
                             print("O diretorio(",operacao[1],")Não Existe!") #imprime informação
                 elif (operacao[0] == "DELETAR"): #se comando for igual a deletar
                       if(os.path.isdir(operacao[1])): #verifica se o diretorio existe
                             os.rmdir(operacao[1]) #apaga o diretorio / comando funciona somente com pastas 
                       else: #caso contrario
                             print ("A pasta(",operacao[1],")Não Existe ! ") #imprime informação na tela
                 elif (operacao[0] == "APAGAR"): #se comando for igual a apagar
                       os.system("del " + operacao[1]) #apaga o arquivo / ultilizo para apagar arquivos
                 else: #caso contrario
                       print("Comando Invalido !") # exibe msg erro
            #fim do bloco com dois comandos de entrada
                        

            #Bloco com três comandos de entrada
            elif len(operacao) == 3: #conta a quantidade de argumentos / se for igual a três entra no bloco
                  if(operacao[0] == "CRIAR"):  #se comando for igual a criar
                        if (operacao[1] == "-d"): #verifica se é p/ criar um diretorio 
                              if(os.path.exists(operacao[2])): #verifica se já existe um diretório com esse nome
                                    print("Já existe um diretório com esse nome !") #imprime a informação na tela
                              else:  #caso contrario
                                    os.mkdir(operacao[2]) #cria o diretório
                        elif (operacao[1] == "-a"): #verifica se é p/ criar um arquivo
                              if(os.path.exists(operacao[2])): #verifica se já existe um arquivo com esse nome
                                    print("Já existe um arquivo com esse nome !") #imprime na tela
                              else: #caso contrario
                                    arquivo = open(operacao[2],"w")#abre/cria o arquivo
                                    arquivo.close() #fecha o arquivo

                  elif(operacao[0] == "INSERIR"): #se o comando for igual a inserir
                        if(os.path.isdir(operacao[2])): #verifica se o arquivo existe
                              arquivo = open(operacao[2],'w') #abre o arquivo
                              texto = "" #define a variavel texto como vazia
                              texto.append(operacao[1]) #adiciona o que o úsuario digitou / na variavel texto
                              arquivo.write(texto)  #adiciona a variavel texto no arquivo
                              arquivo.close() #fecha o arquivo
                              
                              arquivo = open(operacao[2],'r') #abre o arquivo / agora como leitura
                              texto = arquivo.read()  #le o arquivo todo para a variavel
                              arquivo.close() #fecha o arquivo
                        else: #caso contrario
                              arquivo = open(operacao[2],"w") #ira criar um novo arquivo
                              arquivo.write(operacao[1]) #insere o texto
                              arquivo.close()#fecha o arquivo
                              arquivo = open(operacao[2],'r') #abre o arquivo para leitura
                              texto = arquivo.read() #le o arquivo
                              arquivo.close() #fecha o arquivo
                              
                              
                  elif(operacao[0] == "RENOMEAR"): #se comando for igual a renomear
                        os.system("ren " + operacao[1]+ " " + operacao[2]) #renomeia o arquivo ou diretorio
                  elif(operacao[0] == "MOVER"): #se comando for igual a mover
                        shutil.move(operacao[1],operacao[2]) #move o do local atual p/ o destino
                  elif(operacao[0] == "COPIAR"): #se comando for igual a copiar
                        shutil.copy(operacao[1],operacao[2]) #copia o arquivo / pasta de destino
                  else:
                        print("Comando Invalido !") #exibe msg erro
            else:
                  print("Comando Invalido !") #exibe msg erro
            #fim do bloco com três comandos
                        
                             
                                                                                             
def ajuda(): #função que imprime a ajuda
      print("COMANDO | DESCRIÇÃO | EXEMPLO \n")
      print("CRIAR | Cria um diretório |  >>> CRIAR -d pasta1")
      print("CRIAR | Cria um arquivo | >>> CRIAR -a arquivo1\n")
      print("INSERIR | Insere um texto em um arquivo | >>> INSERIR ..... arquivo1\n")
      print("LISTAR | Lista arquivos e diretorios da pasta atual | >>> LISTAR")
      print("LISTAR | Lista arquivos e diretorios da pasta desejada | >>> LISTAR pasta1\n")
      print("COPIAR | Copia arquivos, para os destinos | >>> COPIAR juca.txt documentos\n")
      print("APAGAR | Apaga um arquivo | >>> APAGAR pasta1\n")
      print("RENOMEAR | Renomeia um arquivo ou diretorio | >>> RENOMEAR pasta1 pasta2\n")
      print("MOVER | Move um arquivo ou diretorio | >>> MOVER pasta2 documentos\n")
      print("DELETAR | Deleta um diretorio | >>> DELETAR pasta2\n")
      print("AJUDA | Lista todos os comandos desta tabela, com descrições | >>> AJUDA\n")
      print("VERSÃO | Imprime a versão do Sistema Operacional | >>> VERSÃO\n")
      print("DATA | Imprime a data do Sistema Operacional | >>> DATA\n")
      print("HORA | Imprime a hora do Sistema Operacional | >>> HORA\n")
      print("LIMPAR | Limpa o conteúdo atual da tela(somente no prompt) | >>> LIMPAR\n")
      print("GOOGLE | Abre o nagegador chrome | >>> GOOGLE\n")
      print("SAIR | Finaliza o progarama | >>> SAIR\n")
      
      
      
def main():
      return interpretador()
main()    
      
