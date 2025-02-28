# Jogo de Adivinhação, aula 02 
## UC: IA

```python
import random
import matplotlib.pyplot as plt

class GameAgent:
    def __init__(self, secret_number,dificuldade, max_attempts=5,):
        self.secret_number = secret_number
        self.max_attempts = max_attempts
        self.attempts = 0
        self.dificuldade = dificuldade
        self.state = "Esperando tentativa"
        self.history = []  # Histórico de tentativas

    def make_guess(self, guess):
        self.attempts += 1
        self.history.append(guess)

        if guess == self.secret_number:
            self.state = "DIVOU VEYRRR!"
            return "Parabéns, veyrr! Você acertou o número, nem amo não."

        elif self.attempts >= self.max_attempts:
            self.state = "cabô"
            return f"Game Over! O número era {self.secret_number}."

        elif guess < self.secret_number:
            self.state = "Tentativa errada (muito baixo)"
            return "O número é maior veyr. Tente novamente, amg."

        else:
            self.state = "Tentativa errada (muito alto)"
            return "O número é menor veyrr. Tente novamente amg."

    def get_dificuldade(self):
        return self.dificuldade

    def set_dificuldade(self, dificuldade):
       self.dificuldade = dificuldade

    def get_history(self):
        return self.history

    def give_dica(self):
        if not self.history:
            return "Nenhuma tentativa ainda."

        ultima_tentativa = self.history[-1]

        if ultima_tentativa <self.secret_number:
            if (self.secret_number - ultima_tentativa) <=5:
              return "TA PERTO MAS TA CHUTANDO BAIXO"
            else:
              return "CHUTANDO BAIXO MANO, AUMENTA ESSE TREM"

        else:
            if (ultima_tentativa - self.secret_number) <=5:
              return "TA PERTO MAS TA CHUTANDO ALTO"
            else:
              return "CHUTANDO ALTO MANO, DIMINUA ESSE TREM"

    def plot_attempts(self):
     plt.figure(figsize=(8, 5))
     plt.plot(range(1, len(agent.history)+ 1), agent.history, marker='o', linestyle='-')
     plt.axhline(y=agent.secret_number, color='r', linestyle='--', label='Número Secreto')
     plt.xlabel('Tentativas')
     plt.ylabel('Valor do Palpite')
     plt.title('Evolução das tentativas do jogador')
     plt.legend()
     plt.show()

# Função para obter a dificuldade do usuário
def get_dificuldade_from_user():
    while True:
        try:
            dificuldade_choice = int(input("Escolha a dificuldade (1-iz, 2-mehh, 3-vey vou kitar): "))
            if dificuldade_choice in [1, 2, 3]:
                if dificuldade_choice == 1:
                    return "iz"
                elif dificuldade_choice == 2:
                    return "mehh"
                else:
                    return "vey vou kitar"
            else:
                print("Escolha inválida. Digite 1, 2 ou 3.")
        except ValueError:
            print("Entrada inválida. Digite um número.")

# Obtendo a dificuldade do usuário
dificuldade_escolhida = get_dificuldade_from_user()

# Criando um agente com a dificuldade escolhida
agent = GameAgent(secret_number=random.randint(1, 100), dificuldade=dificuldade_escolhida)


while agent.state not in ["DIVOU VEYRRR!", "cabô"]:
   guess = int(input("Digite um número: "))
   print(agent.make_guess(guess))
   print("Histórico das suas vergonhas:", agent.get_history())
   print("Dica porque c é noob demais:", agent.give_dica())
   print(agent.state)

   if agent.state in ["DIVOU VEYRRR!", "cabô"]:
    agent.plot_attempts()

```
