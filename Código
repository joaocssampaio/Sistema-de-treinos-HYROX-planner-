import os 
import platform

arquivo = open("Sistema de Treinos.txt", "a")
arquivo.close()

def clear():
    OS = platform.system()
    if OS == "Darwin":
        os.system("clear")
    else:
        os.system("cls")

clear()

def abrir_leitura():
    treino = open("Sistema de Treinos.txt", "r")
    conteudo = treino.read()
    treino.close()

    return conteudo

def pergunta():
    while True:
        resposta = input("Você quer continuar? s/n \nRESPOSTA: ").lower()

        if resposta == "s":
            clear()
            return True

        elif resposta == "n":
            return False
        else: 
            print("RESPOSTA INVÁLIDA!") 

def nomeDOtreino(conteudo):
    while True:
        try:
            nome_treino = input("Digite o nome do treino: ")
        except:
            if f"NOME DO TREINO: {nome_treino.upper().strip()}" in conteudo:
                print("O treino ja existe!\n")
                continue
        else:
            clear()
            break
    return nome_treino

def tipoDEtreino():
    while True:
        try:
            tipo_treino = int(input("[1] CORRIDA / [2] FORÇA / [3] SIMULADO HYROX \n\nDigite o tipo de treino entre os disponíveis: " ))
            
            if tipo_treino == 1:
                tipo = "CORRIDA"
                
            elif tipo_treino == 2:
                tipo = "FORÇA"
            
            elif tipo_treino == 3:
                tipo = "SIMULADO HYROX"
            
        except (ValueError, TypeError): 
            clear()
            print("Resposta inválida!")
            continue
        else:
            break
    clear()
    return tipo

def intensidadeDEtreino():
    while True:
        try:
            intensidade_treino = int(input("[1] - LEVE / [2] - MODERADO / [3] - PESADO"
            "\nDigite o número de intensidade: "))

            if intensidade_treino == 1:
                intensidade_final = "Treino Leve"

            elif intensidade_treino == 2:
                intensidade_final = "Treino Moderado"

            elif intensidade_treino == 3:
                intensidade_final = "Treino Pesado"

        except:
            clear()
            print("Resposta Inválida!")
            continue
        
        else:
            break
    clear()
    return intensidade_final
    
def validar_data():
    from datetime import datetime
    while True:
        try:
            data = input("Digite a data do treino (dd/mm/aaaa): ")
            data_formatada = datetime.strptime(data, "%d/%m/%Y")

            clear()
            return data
                
        except ValueError:
            clear()
            print("Data inválida! Use o formato dd/mm/aaaa.\n")
            continue

def controledesempenho(nomedotreino):

    desemp = {} 

    # ================= ABRE O ARQUIVO ===================
 
    file = open("Sistema de Treinos.txt", "r")
    conteudo = file.read()
    file.close()

    treinos = conteudo.split("\n\n")

    if "EXERCICIOS:" in treinos[-1]: 

        desempenhos = (treinos[-1]).split("\n---\n")

        achou = False
        for i in range(1, len(desempenhos)):
            if nomedotreino + "\n" in desempenhos[i]:
                esse_desempenho = desempenhos[i]
                index = i
                achou = True
                break
        
        if achou:

            linhas = esse_desempenho.split("\n")
            
            i = 1
            while i <= len(linhas)-4:
                desemp[linhas[i]] = [linhas[i+1].split("\t")[2:-1],
                                    linhas[i+2].split("\t")[1:-1],
                                    linhas[i+3].split("\t")[2:-1],
                                    linhas[i+4].split("\t")[1:-1]]
                i += 5
        
        else:
            desempenhos.append("valor que vai ser trocado dps")
            index = len(desempenhos)-1
                
    else:
        desempenhos = ["EXERCICIOS:", "valor que vai ser trocado dps"]
        index = 1
        treinos.append(desempenhos)


    # ====================== ADICIONAR NOVA LEITURA / CRIAR EXERCICIO =============

    def add(exercicio):
        #exercicio é o nome do exercicio

        if exercicio not in desemp.keys():
            desemp[exercicio] = [[],[],[],[]] #se o exercicio não existir ainda, criar uma matriz pra ele

        tempo = input("Insira o tempo: ")
        dist = input("Insira a distância: ")
        carga = input("Insira a carga: ")
        rep = input("Insira a quantidade de repetições: ")

        desemp[exercicio][0].append(tempo)
        desemp[exercicio][1].append(dist)
        desemp[exercicio][2].append(carga)
        desemp[exercicio][3].append(rep)

        print(f"Exercício {exercicio} atualizado!\n")

    # ====================== SALVAR MATRIZ =========================

    def salvarmatriz():
        dados = nomedotreino

        for exercicio in desemp.keys():
            dados += "\n" + exercicio.upper()

            dados += ("\nTempos:\t\t")
            for d in desemp[exercicio][0]:
                dados += (d + "\t")

            dados += ("\nDistâncias:\t")
            for d in desemp[exercicio][1]:
                dados += (d + "\t")

            dados += ("\nCargas:\t\t")
            for d in desemp[exercicio][2]:
                dados += (d + "\t")

            dados += ("\nRepetições:\t")
            for d in desemp[exercicio][3]:
                dados += (d + "\t")
        
        desempenhos[index] = dados

        treinos.pop()
        treinos.append("\n---\n".join(desempenhos))

        conteudo = "\n\n".join(treinos)


        file = open("Sistema de Treinos.txt", "w")
        file.write(conteudo)
        file.close()
        
    # ====================== LOOP PRINCIPAL =========================

    print("EXERCICIOS e Controle de Desempenho\n")

    cmd = "S"
    while True:
        if cmd == "S":
            clear()
            nome = input("Digite o nome do exercício que deseja adicionar/atualizar: ").upper()

            add(nome)
        elif cmd == "N":
            salvarmatriz()
            print("Encerrando programa...")
            clear()
            break
        else:
            print("comando não reconhecido.")
        
        cmd = input("Deseja continuar? (S/N) ").upper()

def calcular_dias_restantes(data_):
    import datetime
    try:
        data_evento = datetime.datetime.strptime(data_.strip(), "%d/%m/%Y").date()
        data_hoje = datetime.date.today()
        diferenca = data_evento - data_hoje
        
        if diferenca.days > 0:
            return f"Faltam {diferenca.days} dias"
        elif diferenca.days == 0:
            return "É HOJE!"
        else:
            return f"Aconteceu há {abs(diferenca.days)} dias"
    except ValueError:
        return "Data inválida"

def adicionar_competicao(comp,data,local,cat):

    status_dias = calcular_dias_restantes(data)
    
    dados_competicao =(f"\n=========={comp}==========\n"
                       f"DATA: {data} \t{status_dias}\n"
                       f"LOCAL: {local}\n"
                       f"CATEGORIA: {cat}\n")
    
    arquivo = open("Competições.txt","a")
    arquivo.write(dados_competicao)
    arquivo.close()



while True:
   print("==========BEM VINDO AO HYROX PLANNER==========\n")
   opcao_escolhida = input("Você deseja:" 
    "\n[1] Adicionar\n"
        "[2] Visualizar treinos\n"
        "[3] Visualizar competições \n"
        "[4] Editar\n"
        "[5] Excluir\n"
        "[6] Controle de Desempenho\n"
        "[7] Adicionar competição \n"
        "[8] Parar"
        "\nRESPOSTA: ")

   clear()

   if opcao_escolhida == "1":
    
        conteudo = abrir_leitura()

        nome_treino = nomeDOtreino(conteudo)

        tipo = tipoDEtreino()

        data_treino = validar_data()

        duracao_treino = input("Digite o tempo de duração: ")
        clear()

        intensidade_final = intensidadeDEtreino()
            
        clear()
        
        treino = open("Sistema de Treinos.txt", "r")
        conteudo = treino.read()
        treino.close()

        treino = open("Sistema de Treinos.txt", "w")

        dados_novos = ("Dados do Treino:" 
                        "\nNOME DO TREINO: " + nome_treino.upper().strip() + 
                        "\nTIPO DE TREINO: " + tipo + 
                        "\nDATA DO TREINO: " + data_treino + 
                        "\nDURAÇÃO DO TREINO: " + duracao_treino +
                        "\nINTENSIDADE DO TREINO: " + intensidade_final)
        
        treinos = conteudo.split("\n\n") # quebra o texto cru do arquivo em uma lista
        if "EXERCICIOS:\n" in treinos[-1]:
            treinos.insert(-1, dados_novos) # coloca os dados novos dentro da lista antes da parte de controle de desempenho
        else:
            treinos.append(dados_novos)
        treino.write("\n\n".join(treinos)) # da .join na lista e sobreescreve o arquivo inteiro

        # isso faz com que o controle de desempenho sempre fique na parte de baixo do arquivo (tem q ser assim pra o meu codigo funcionar)

        clear()
        print("Treino Adicionado com Sucesso! \n\n")
        treino = open("Sistema de Treinos.txt", "r")
        treino.close()


   elif opcao_escolhida == "2":
        clear()
        treino = open("Sistema de Treinos.txt", "r")
        print(treino.read())
        treino.close()
        if not pergunta():
            break


   elif opcao_escolhida == "3":
        clear()
        print("==========COMPETIÇÕES==========")

        try:
            arquivo_comp = open("Competições.txt","r")
            conteudo_comp = arquivo_comp.read()
            arquivo_comp.close()

            if conteudo_comp.strip() =="":
                print("Nenhuma competição cadastrada")
            else:
                print(conteudo_comp)

        except FileNotFoundError:
            print("Nenhuma competição cadastrada ainda.")
                  
        if not pergunta():
            break


   elif opcao_escolhida == "4":
        conteudo = abrir_leitura()
        treinos = conteudo.split("\n\n")

        while True:
            try:
                treino_antigo = input("Digite qual treino deseja editar: ")
            except:    
                if f"NOME DO TREINO: {treino_antigo.upper()}\n" not in conteudo:
                    print("Treino Inexistente!!\n\n")
                    continue
            else:
                clear()
                break
            
        treino_novo = nomeDOtreino(conteudo)

        # ========================================
        # Essa parte do código procura o treino antigo no controle de desempenhos

        if "EXERCICIOS:" in treinos[-1]: 

            desempenhos = (treinos[-1]).split("\n---\n")

            achou = False
            for o in range(1, len(desempenhos)):
                if treino_antigo.lower() + "\n" in desempenhos[o]:
                    esse_desempenho = desempenhos[o]
                    index = o
                    achou = True
                    break
            
            if achou:
                linhas = esse_desempenho.split("\n")
                linhas[0] = treino_novo.lower().strip() # atualiza a primeira linha de esse_desempenho

                desempenhos[o] = "\n".join(linhas) # junta as linhas e coloca em desempenhoS

                treinos[-1] = "\n---\n".join(desempenhos) # atualiza o último índice de treinos

                # e veja só que maravilha! eu não presciso colocar < "\n\n".join(treinos) > no arquivo de volta, pq o código de vini já faz isso pra mim!

        # ========================================

        tipo = tipoDEtreino()

        data_nova = validar_data()
        clear()

        duracao_nova = input("Digite o novo tempo de duração: ")
        clear()

        intensidade_final = intensidadeDEtreino()

        dados_novos = ("Dados do Treino: "
                       "\nNOME DO TREINO: " + treino_novo.upper().strip() + 
                       "\nTIPO DE TREINO: " + tipo +
                       "\nDATA DO TREINO: " + data_nova + 
                       "\nDURAÇÃO DO TREINO: " + duracao_nova + 
                       "\nINTENSIDADE DO TREINO: " + intensidade_final)

        for i in range(len(treinos)):
            if "NOME DO TREINO: " + treino_antigo.upper().strip() + "\n" in treinos[i]: # o \n impede que vc mude treinos com nomes parecidos (Ex: braços A, braços B)
                treinos[i] = dados_novos
                break

        novo_conteudo = "\n\n".join(treinos)

        treino = open("Sistema de Treinos.txt", "w")
        treino.write(novo_conteudo)
        treino.close()
        clear()
        print("Treino editado com Sucesso!")

        if not pergunta():
            break


   elif opcao_escolhida == "5":
        conteudo = abrir_leitura()
        treinos = conteudo.split("\n\n")
        
        while True: 
            try:
                treino_excluir = input("Digite o treino que deseja excluir: ")
            except:  
                if f"NOME DO TREINO: " + treino_excluir.upper().strip() not in conteudo:
                    clear()
                    print("Treino inexistente!\n")
                    continue
            else:
                clear()
                break
        
        # ========================================
        # Essa parte do código procura o treino antigo no controle de desempenhos

        if "EXERCICIOS:" in treinos[-1]: 

            desempenhos = (treinos[-1]).split("\n---\n")

            achou = False
            for o in range(1, len(desempenhos)):
                if treino_excluir.lower() + "\n" in desempenhos[o]:
                    #esse_desempenho = desempenhos[i] #nesse caso, como eu só presciso deletar, não tem motivo pra dividir esse desempenho em linhas
                    index = o
                    achou = True
                    break
            
            if achou:
                
                if len(desempenhos) <= 2: 
                    treinos.pop(-1) # se desempenhos for ["EXERCICIOS:", desempenhos[i]], é melhor deletar tudo logo do que deixar só "EXERCICIOS:" no final do arquivo

                else:
                    desempenhos.pop(o) # remove esse desempenho
                    
                    treinos[-1] = "\n---\n".join(desempenhos) # atualiza o último índice de treinos

                    # e, denovo, nn prescisa atualizar o arquivo aqui

        # ========================================

        conjunto_fica = []
        
        for i in range(len(treinos)):
            if "NOME DO TREINO: " + treino_excluir.upper().strip() in treinos[i]:
                continue
            else:
                conjunto_fica.append(treinos[i])
                
        conjunto_fica = "\n\n".join(conjunto_fica)
        
        treino = open("Sistema de Treinos.txt", "w")
        treino.write(conjunto_fica)
        treino.close()
        print("Treino Excluído Com Sucesso!\n\n")
        

   elif opcao_escolhida == "6":
        treinoCD = input("Digite um treino para adicionar um desempenho: ")

        treino = open("Sistema de Treinos.txt", "r")
        conteudo = treino.read()
        if "NOME DO TREINO: " + treinoCD.upper() in conteudo:
            # só deixa adicionar um treino ao controle de desempenho se ele existir no crude,
            # ⚠️ mas não impede o nome de ficar diferente aqui se o treino original for renomeado ou deletado
            controledesempenho(treinoCD)
        else:
            print("Treino inexistente, adicione ele pelo CRUDE primeiro!")
        


   elif opcao_escolhida == "7":
        import datetime
        nome_comp = input("Digite o nome da competição:")
        while True:
            data_comp = input("Digite a data da competição (DD/MM/AAAA): ")
            try:
                datetime.datetime.strptime(data_comp.strip(), "%d/%m/%Y").date()
                break

            except ValueError:
                print("Data inválida ou fora do padrão (DD/MM/AAAA). Tente novamente!\n")

        local_comp = input("Digite o local da competição:")
        cat_comp = input("Digite a categoria da competição:")

        adicionar_competicao(nome_comp,data_comp,local_comp,cat_comp)

        print("Competição adicionada com sucesso!\n\n")


   elif opcao_escolhida == "8":
        print("Programa Finalizado!")
        break


   else:
        print("Opção inválida!")
        if not pergunta():
            break

