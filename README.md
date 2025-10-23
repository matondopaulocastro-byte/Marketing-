# Marketing-
A mobile Marketing app
import json
import os

DATA_FILE = "data/contatos.json"

# Lista de produtos
produtos = [
    {"id": 1, "nome": "Produto A", "preco": 10.0},
    {"id": 2, "nome": "Produto B", "preco": 20.0},
    {"id": 3, "nome": "Produto C", "preco": 30.0}
]

def load_contatos():
    if not os.path.exists(DATA_FILE):
        return []
    with open(DATA_FILE, "r") as f:
        return json.load(f)

def save_contatos(contatos):
    os.makedirs("data", exist_ok=True)
    with open(DATA_FILE, "w") as f:
        json.dump(contatos, f, indent=2)

def mostrar_produtos():
    print("\n--- Produtos Disponíveis ---")
    for p in produtos:
        print(f"{p['id']}: {p['nome']} - ${p['preco']}")
    print("----------------------------\n")

def coletar_contato(contatos):
    nome = input("Digite seu nome: ")
    email = input("Digite seu email: ")
    contatos.append({"nome": nome, "email": email})
    save_contatos(contatos)
    print("Cadastro realizado com sucesso!\n")

def main():
    contatos = load_contatos()
    while True:
        print("1 - Mostrar Produtos")
        print("2 - Cadastrar Contato")
        print("3 - Ver Contatos Salvos")
        print("4 - Sair")
        escolha = input("Escolha uma opção: ")

        if escolha == "1":
            mostrar_produtos()
        elif escolha == "2":
            coletar_contato(contatos)
        elif escolha == "3":
            print("\n--- Contatos Salvos ---")
            print(json.dumps(contatos, indent=2))
            print("-----------------------\n")
        elif escolha == "4":
            print("Saindo do app...")
            break
        else:
            print("Opção inválida. Tente novamente.\n")

if __name__ == "__main__":
    main()
