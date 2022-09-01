# JOGO-LUDO-EM-C 
/*Estou com dificuldades em dar andamento no jogo, pois gostaria de saber como andar com a STRUCT na matriz de tabuleiro char( aceito sugestões se for melhor fazer tabuleiro de tipo inteiro ou algo do tipo) minha duvida é em como andar com a struct na matriz.*/
a logica do game é a seguinte 
O tabuleiro quadrado tem um percurso em forma de cruz e cada jogador tem quatro peões. Um dado define os movimentos. Os peões de cada jogador começam na base de mesma cor. O objetivo do jogo é ser o primeiro a levar seus 4 peões a dar uma volta no tabuleiro e a chegar no ponto final marcado com sua cor.

#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <string.h>

typedef struct
{
	char nome[10];
	char peao[10];
}jogador;

void menu();
int players();
jogador*alocaJogador();
jogador*dadosjogadores();
void tabuleiro();
void dado();
void game();

int main()
{	
	jogador *p;
	menu();
	int quant = players();
	p = alocaJogador(quant);
	p= dadosjogadores(p,quant);
	game(p,quant);
  free(p);
	return 0;	
}

void menu()
{	
	int op;
	printf("*******************BEM-VINDOS AO JOGO LUDO*******************\n");
	printf("\n                         MENU:\n                         1-Start game\n                         2-Exit");
	scanf("%d",&op);
	//system("pause");
	system("cls");	
}

int players() //------------------------função para usuario digitar quantidade de jogadores que participarao no jogo
{
	int i,op;
	printf("Digite a quantidade de jogadores:");
	scanf("%d",&op);
	return op;
}

jogador*alocaJogador(int quant) //-----------------------função para alocar as struct dinamicamente
{
	jogador *x = ( jogador*) malloc ( quant*sizeof ( jogador ));
	if(x == NULL)
	{
		exit(1);
	}
	return x;	
}

jogador*dadosjogadores(jogador*x,int quant)//----------------função para endereçar os dados dos jogadores(struct jogador)
{                                          //----------------cada peao será nomeado de acordo com a cor que o usuario colocar(aceito sugestões)
	int i;
	for(i=0;i<quant;i++)
	{
		printf("Digite o nome do jogador %d",i);
		scanf("%s",x[i].nome);
		printf("Digite a cor do peao do jogador %d",i);
		scanf("%s",x[i].peao);
		printf("jogador %d de nome %s e do time de cor %s\n\n",i,x[i].nome,x[i].peao);
	}
	system("pause");
	system("cls");
	return x;	
}

void tabuleiro()
{
	int i,j;
	char tab[15][15] = {{' ',' ',' ',' ',' ',' ','-','-','-',' ',' ',' ',' ',' ',' '},
						{' ',' ',' ',' ',' ',' ','-','#','-',' ',' ',' ',' ',' ',' '},
						{' ',' ',' ',' ',' ',' ','-','#','-',' ',' ',' ',' ',' ',' '},
						{' ',' ',' ',' ',' ',' ','-','#','-',' ',' ',' ',' ',' ',' '},
						{' ',' ',' ',' ',' ',' ','-','#','-',' ',' ',' ',' ',' ',' '},
						{' ',' ',' ',' ',' ',' ','-','#','-',' ',' ',' ',' ',' ',' '},
						{'-','-','-','-','-','-','-','#','-','-','-','-','-','-','-'},
						{'-','#','#','#','#','#','#','+','#','#','#','#','#','#','-'},
						{'-','-','-','-','-','-','-','#','-','-','-','-','-','-','-'},
						{' ',' ',' ',' ',' ',' ','-','#','-',' ',' ',' ',' ',' ',' '},
						{' ',' ',' ',' ',' ',' ','-','#','-',' ',' ',' ',' ',' ',' '},
						{' ',' ',' ',' ',' ',' ','-','#','-',' ',' ',' ',' ',' ',' '},
						{' ',' ',' ',' ',' ',' ','-','#','-',' ',' ',' ',' ',' ',' '},
						{' ',' ',' ',' ',' ',' ','-','#','-',' ',' ',' ',' ',' ',' '},
						{' ',' ',' ',' ',' ',' ','-','-','-',' ',' ',' ',' ',' ',' '}};
						
	for (i=0;i<15;i++)
	{
		for(j=0;j<15;j++)
		{
			printf("%c",tab[i][j]);	
		}
		printf("\n");
	}					
}

void dado()
{	
	int i,op,dad = rand()%6+1;
	srand(time(NULL));
	printf("DADO = %d",dad);		
}

void game(jogador*x,int quant)
{
	tabuleiro();
	int i,op,rodada=0;
	do{
		for(i=0;i<quant;i++)
		{
			printf("jogador %s aperte tecle 1 para jogar dado:",x[i].nome);
			scanf("%d",&op);
			if(op == 1)
			{
				dado();	
			}	
		}
		rodada++;
		printf("\nrodada %d terminada\n\n",rodada);
		
	}while(op!=0);
}
