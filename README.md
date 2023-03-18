# Campo-Minado
Campo minado desenvolvido para trabalho escolar, quanto em visualG, quanto em C#. serão comentadas as alterações.
Descrição informativa: Campo minado é um popular jogo de computador para um jogador. Foi inventado por Robert Donner em 1989 e tem como objectivo revelar um campo de minas sem que alguma seja detonada.

//------------------------------------------------------------------------------
Algoritmo "Campo Minado"
Var
   Tabuleiro: vetor [1..10,1..10] de inteiro
   i, j, NumeroMinas, Linha, Coluna, EspacosLiberados, Status, JogadasRestantes: inteiro

Inicio
//------------------------------------------------------------------------------
   // define o tamanho do tabuleiro e o número de minas
   NumeroMinas <- 10
   EspacosLiberados <- 0
   JogadasRestantes <- 90
   Status <- 0
//------------------------------------------------------------------------------
   // cria o tabuleiro
   para i de 1 ate 10 faca
      para j de 1 ate 10 faca
         Tabuleiro[i,j] <- 0
      fimpara
   fimpara
//------------------------------------------------------------------------------
   // colocar as minas
   para i de 1 ate NumeroMinas faca
      repita
          Linha <- randi(9)+1
          Coluna <- randi(9)+1
      ate Tabuleiro[Linha, Coluna] = 0
      Tabuleiro[Linha, Coluna] <- 9
   fimPara
//------------------------------------------------------------------------------
   // loop principal do jogo
   enquanto (Status = 0) faca
//------------------------------------------------------------------------------
      // mostrar o tabuleiro antes das jogadas
      para i de 1 ate 10 faca
         para j de 1 ate 10 faca
            se (Tabuleiro[i,j] >= 10) entao
               escreva(" *")
            senao
                  se (Tabuleiro[i,j] = 9) entao
                     escreva(" -")
                  senao
                     escreva(Tabuleiro[i,j])
                  fimse
            fimse
         fimpara
         escreval("")
      fimpara
//------------------------------------------------------------------------------
      // solicitar jogada do jogador
      escrevaL("Digite a linha e a coluna que deseja revelar (ex: 3 5):")
      leia(Linha, Coluna)
//------------------------------------------------------------------------------
      // verificar se a jogada é válida
      se (Linha < 1) ou (Linha > 10) ou (Coluna < 1) ou (Coluna > 10) entao
         escrevaL("Jogada inválida, tente novamente.")
      senao
         se (Tabuleiro[Linha, Coluna] >= 10) entao
            escrevaL("Você acertou uma mina! Fim de jogo.")
            Status <- 1
         senao
              // revelar espaço selecionado e verificar se o jogador ganhou
              Tabuleiro[Linha, Coluna] := Tabuleiro[Linha, Coluna] + 10
              EspacosLiberados <- EspacosLiberados + 1
              JogadasRestantes <- JogadasRestantes - 1
              se (EspacosLiberados = 90 - NumeroMinas) entao
                 escrevaL("Parabéns! Você venceu o jogo.")
                 Status <- 2
              senao
                   se (JogadasRestantes = 0) entao
                      escrevaL("Você esgotou todas as jogadas! Fim de jogo.")
                      Status <- 1
                   fimse
             fimse
          fimse
      fimse
   fimenquanto
fimalgoritmo
