# Sistema Bancário (Desafio) — README

Um sistema bancário em Python criado para fins didáticos, implementando operações básicas de conta corrente, controle de clientes, histórico de transações e menu interativo no terminal.

## 🏦 Funcionalidades principais
- Criar cliente (Pessoa Física) com nome, CPF, data de nascimento e endereço.  
- Criar conta corrente associada a um cliente.  
- Depositar e sacar valores com validações.  
- Exibir extrato completo com histórico de transações.  
- Listar todas as contas existentes.  
- Selecionar qual conta usar (caso o cliente possua mais de uma).  
- Log simples de operações via decorador `@log_transacao`.

## ⚙️ Requisitos
- **Python 3.8+**  
- Nenhuma dependência externa.

## 🧱 Estrutura do código
### Classes principais
- **Cliente / PessoaFisica** → representam o cliente, com dados pessoais e lista de contas.  
- **Conta / ContaCorrente** → controlam saldo, saques, depósitos, limites e número de saques diários.  
- **Historico** → armazena todas as transações realizadas, com tipo, valor e data/hora.  
- **Transacao, Saque, Deposito** → abstraem as operações de movimentação e registram no histórico.  
- **ContasIterador** → itera sobre a lista de contas de forma formatada (para o menu de listagem).

## 🔁 Função atualizada — Seleção de conta
A função `recuperar_conta_cliente()` foi **corrigida e aprimorada** para permitir que o usuário escolha qual conta deseja usar ao realizar transações.  

```python
def recuperar_conta_cliente(cliente):
    if not cliente.contas:
        print("\n@@@ Cliente não possui conta! @@@")
        return

    if len(cliente.contas) == 1:
        return cliente.contas[0]

    print("\n=== Contas do Cliente ===")
    for i, conta in enumerate(cliente.contas, start=1):
        print(f"[{i}] Agência: {conta.agencia} | Conta: {conta.numero} | Saldo: R$ {conta.saldo:.2f}")

    while True:
        try:
            opcao = int(input("Escolha o número da conta: "))
            if 1 <= opcao <= len(cliente.contas):
                return cliente.contas[opcao - 1]
            else:
                print("\n@@@ Opção inválida, tente novamente. @@@")
        except ValueError:
            print("\n@@@ Entrada inválida! Digite apenas números. @@@")
```

## ▶️ Como executar
1. Salve o código em um arquivo, por exemplo `bank.py`.  
2. Execute no terminal:
```bash
python bank.py
```
3. Utilize o menu para interagir com o sistema:

| Comando | Função |
|----------|---------|
| `nu` | Criar novo usuário |
| `nc` | Criar nova conta |
| `d` | Depositar |
| `s` | Sacar |
| `e` | Ver extrato |
| `lc` | Listar contas |
| `q` | Sair |

## ⚠️ Observações
- Cada cliente pode possuir **várias contas**.  
- O limite padrão de saque é de **R$500** por operação.  
- O número máximo de saques diários é **3**.  
- Caso o cliente tente realizar mais de 2 transações no mesmo dia, é exibido um aviso.
