#include <iostream>
#include <stdio.h>
#include <string.h>
#include <time.h>

using namespace std;

struct cad {
    int id;
    char nome[30];
    char especie[20];
    char raca[20];
    char sexo, status;
    int idade;
    char carac[100];
    struct cad *prox, *ant;
    char data_cad[30];
    char data_alt[30];
};

void loadFile(struct cad **inicio);
void saveFile(struct cad *inicio);
void registerAnimal(struct cad **inicio); 
void insertNode(struct cad **inicio, struct cad *auxnovo, char nome[30]);
void searchName(struct cad *inicio);
void printList(struct cad *inicio);
void searchSpecies(struct cad *inicio);
void searchSpeciesAndBreed(struct cad *inicio);
void searchSpeciesBreedAndSex(struct cad *inicio);
void counting(struct cad *inicio);
void countingOfBreed(struct cad *inicio);
void changeRegister(struct cad **inicio);
void removeAnimal(struct cad **inicio);
void changeAnimalStatus(struct cad **inicio);
void changeStatus(struct cad **inicio, int id, char newStatus);
void clearScreen();

int main() {
  setlocale(LC_ALL, "portuguese");

  int opcao;
  struct cad *inicio = NULL;

  loadFile(&inicio);
  
  do{
    cout << "MENU: \n";
    cout << "1. Cadastrar novo animal.\n";
    cout << "2. Alterar informações do cadastro.\n";
    cout << "3. Buscar um animal pelo nome.\n";
    cout << "4. Buscar animais por espécie.\n";
    cout << "5. Buscar animais por espécie e raça.\n";
    cout << "6. Buscar animais por espécie, raça e sexo.\n";
    cout << "7. Quantidade de animais cadastrados.\n";
    cout << "8. Quantidade de animais por espécie.\n";
    cout << "9. Listar cadastro de todos os animais.\n";
    cout << "10. Remover animal da lista.\n";
    cout << "11. Alterar status de um animal.\n";
    cout << "12. Limpar tela.\n";
    cout << "0. SAIR\n";

    cout << "Digite a opção desejada: ";
    cin >> opcao;

    switch(opcao){
      case 1: registerAnimal(&inicio); break;
      case 2: changeRegister(&inicio); break;
      case 3: searchName(inicio); break;
      case 4: searchSpecies(inicio); break;
      case 5: searchSpeciesAndBreed(inicio); break;
      case 6: searchSpeciesBreedAndSex(inicio); break;
      case 7: counting(inicio); break;
      case 8: countingOfBreed(inicio); break;
      case 9: printList(inicio); break;
      case 10: removeAnimal(&inicio); break;
      case 11: changeAnimalStatus(&inicio); break;
      case 12: clearScreen(); break;
    }
  }
  while(opcao!=0);

  saveFile(inicio);

  return 0;
}

void clearScreen(){
  system("clear");
}

void loadFile(struct cad **inicio) {


  cout << "Carregando cadastros..." << endl;

  FILE *arquivo = fopen("cadastros.txt", "r");

  if(arquivo == NULL) {
    cout << "Nenhum cadastro encontrado." << endl;
    return;
  }

  struct cad aux2;

  while(fread(&aux2, sizeof(struct cad), 1, arquivo)) {

    struct cad *aux = (struct cad*)malloc(sizeof(struct cad));

    strcpy(aux->nome, aux2.nome);
    strcpy(aux->especie, aux2.especie);
    strcpy(aux -> raca, aux2.raca);
    aux -> sexo = aux2.sexo;
    aux -> status = aux2.status;
    aux -> idade = aux2.idade;
    strcpy(aux -> carac, aux2.carac);
    aux -> id = aux2.id;

    strcpy(aux -> data_cad, aux2.data_cad);
    strcpy(aux -> data_alt, aux2.data_alt);
    
    insertNode(inicio, aux, aux->nome);
  }
  remove("cadastros.txt");
}

void saveFile(struct cad *inicio) {
  FILE *arquivo = fopen("cadastros.txt", "w+");
  
  struct cad *aux = inicio;
    
  while(aux != NULL) {

    int x = 10;

    struct cad aux2;
    strcpy(aux2.nome, aux->nome);
    strcpy(aux2.especie, aux->especie);
    strcpy(aux2.raca, aux -> raca);
    aux2.sexo = aux -> sexo;
    aux2.status = aux -> status;
    aux2.idade = aux -> idade;
    strcpy(aux2.carac, aux -> carac);
    aux2.id = aux -> id;
    strcpy(aux2.data_cad, aux -> data_cad);
    strcpy(aux2.data_alt, aux -> data_alt);

    fwrite (&aux2, sizeof(struct cad), 1, arquivo);
    aux = aux -> prox;
  }
  fclose(arquivo);
}

bool isFemale(char c) {
  if(c == 'F') {
    return true;
  } else {
    return false;
  }
}

bool isAdopted(char c) {
  if(c == 'A') {
    return true;
  } else {
    return false;
  }
}

void upper(char c[]) {
  for (int a = 0; a<=strlen(c); a++){
    c[a]=toupper(c[a]);
  }
}

char getStatus() {
  char s;
  do {
    cout << "Digite [A] para 'ADOTADO' e [N] para 'NÃO ADOTADO':\n";
    cin >> s;

    s=toupper(s);
  }while(s != 'A' && s != 'N');
  return s;
}

void printList(struct cad *inicio) {

    cout << "Você deseja listar os animais ADOTADOS ou NÃO ADOTADOS?" << endl;

    char s = getStatus();
    
    printf("\nCadastros:\n");
    
    struct cad *aux = inicio;

    if(aux==NULL){
      cout << "\n\nNão existe nenhum cadastro na lista.\n\n";
    }
    
    while(aux != NULL) {

      if(aux -> status == s) {
        cout << "\nID: " << aux->id << "\n";
        cout << "Nome: " << aux->nome << "\n"; 
        cout << "idade: " << aux->idade << "\n";
        cout << "Sexo: " << aux->sexo << "\n";
        cout << "Status: " << (isAdopted(aux -> status) ? "Adotado" : "Não adotado") << "\n";
        cout << "Espécie: " << aux->especie << "\n";
        cout << "Raça: " << aux->raca << "\n";
        cout << "Características gerais: " << aux->carac << "\n";
      cout << "Data de cadastro: " << aux->data_cad << "\n";
      cout << "Data de alteração: " << aux->data_alt << "\n";

      }
      aux = aux -> prox;
    }

    cout << "\nFim da lista de cadastros.\n";
}

void getEspecie(char especie[20]) {
  int x;
  cout << "Qual é a espécie do animal?\n";
  cout << "1. Canino\n";
  cout << "2. Felino\n";
  cout << "3. Roedor\n";
  cout << "4. Réptil\n";
  cout << "5. Outros\n";
  cin >> x;
  switch(x) {
    case 1:
      strcpy(especie, "CANINO");
    break;
    case 2:
      strcpy(especie, "FELINO");
    break;
    case 3:
      strcpy(especie, "ROEDOR");
    break;
    case 4:
      strcpy(especie, "RÉPTIL");
    break;
    default:
      strcpy(especie, "OUTROS");
    break;
  }
}

void getSexo(char *sexo) {
  char s;
  do {
    cout << "Qual é o sexo do animal? Escolha entre [F] e [M]:\n";
    cin >> s;

    s=toupper(s);
  }while(s != 'F' && s != 'M');
  (*sexo) = s;
}

void getNome(char nome[30]) {
  cout << "Qual o nome do animal?\n";
  cin.ignore();
  cin.getline(nome, 30);

  upper(nome);
}

void getRaca(char sexo, char nome[30], char raca[20]) {
  if(nome == NULL || sexo == 'N') {
    cout << "Qual a raça do animal?\n";
  } else {
    cout << "Qual a raça d" << (isFemale(sexo) ? "a " : "o ") << nome << "?\n";
  }
  cin.getline(raca, 20);
  
  upper(raca);
}

void getIdade(char sexo, char nome[30], int *idade) {
  int i;
  cout << "Qual a idade d" << (isFemale(sexo)? "a " : "o ") << nome << "?\n";
  cin >> i;
  (*idade) = i;
}

void getCarac(char sexo, char nome[30], char carac[300]) {
  cout << "Quais as características d" << (isFemale(sexo)? "a " : "o ") << nome << "?\n";
  cin.ignore();
  cin.getline(carac, 100);

  upper(carac);
}

void registerAnimal(struct cad **inicio) {
  
  char especie[20], sexo, raca[20], nome[30], carac[100], status;
  int idade, id;
  struct tm data;
  time_t atual;
  atual = time(NULL);
  data = *localtime(&atual);
  
  getEspecie(especie);

  getSexo(&sexo);

  getNome(nome);

  getRaca(sexo, nome, raca);

  getIdade(sexo, nome, &idade);

  getCarac(sexo, nome, carac);

  status = 'N';

  bool finalizar = false;

  do {

    cout << "\n\tFicha técnica d" << (isFemale(sexo) ? "a " : "o ") << nome << ":\t\n" << endl;
    cout << "- Espécie: " << especie << endl;
    cout << "- Sexo: " << (isFemale(sexo) ? "FÊMEA" : "MACHO") << endl;
    cout << "- Raça: " << raca << endl;
    cout << "- Idade: " << idade << endl;
    cout << "- Características gerais: " << carac << endl << endl;

    char resposta;

    do {
      cout << "As informações estão corretas?" << endl;
      cout << "Digite [S] ou [N]: ";
      cin >> resposta;
      resposta=toupper(resposta); 

    }while(resposta != 'S' && resposta != 'N');
    
    if(resposta == 'S') {

      finalizar = true;

      //INSERIR NÓ
      struct cad *contador = (*inicio);
  
      int id = 1;

      while(contador!=NULL){
        id = id + 1;
        contador = contador -> prox;
      }

      struct cad *auxnovo = (struct cad*)malloc(sizeof(struct cad));
      strcpy(auxnovo -> nome, nome);
      strcpy(auxnovo -> especie, especie);
      strcpy(auxnovo -> raca, raca);
      auxnovo -> sexo = sexo;
      auxnovo -> status = status;
      auxnovo -> idade = idade;
      strcpy(auxnovo -> carac, carac);
      auxnovo -> id = id;
      strcpy(auxnovo -> data_cad, ctime(&atual));
      strcpy(auxnovo -> data_alt, ctime(&atual));

      insertNode(inicio, auxnovo, nome);

    } else {

      finalizar = false;

      cout << "O que você deseja alterar?" << endl;

      cout << "1. Nome.\n";
      cout << "2. Espécie.\n";
      cout << "3. Sexo.\n";
      cout << "4. Raça.\n";
      cout << "5. Idade.\n";
      cout << "6. Características gerais.\n";
      cout << "7. Nada.\n";

      int x;
      cin >> x;

      switch (x) {
        case 1:
        getNome(nome);
        cout << "Nome do animal alterada para: " << nome << "." << endl;
        break;
        case 2:
          getEspecie(especie);
          cout << "Espécie do animal alterada para: " << especie << "." << endl;
        break;
        case 3:
          getSexo(&sexo);
          cout << "Sexo do animal alterado para: " << (isFemale(sexo) ? "Fêmea" : "Macho") << "." << endl;
        break;
        case 4:
          getRaca(sexo, nome, raca);
          cout << "Raça do animal alterada para: " << raca << "." << endl;
        break;
        case 5:
          getIdade(sexo, nome, &idade);
          cout << "Idade do animal alterara para: " << idade << "." << endl;
        break;
        case 6:
          getCarac(sexo, nome, carac);
          cout << "Características do animal alterara para: " << carac << "." << endl;
        break;
      }

    }

  }while(!finalizar);

}

void insertNode(struct cad **inicio, struct cad *auxnovo, char nome[30]) {
  struct cad *aux = (*inicio);
  if (aux==NULL){
         auxnovo->prox=(*inicio);
         auxnovo->ant=NULL;
         (*inicio)=auxnovo;
         return;
      }

      int compare = strcmp(aux->nome, nome);

      if(compare==0){
        while(aux->nome!=nome || aux->nome==nome){
          if(aux->prox==NULL){
          aux->prox=auxnovo;
          auxnovo->ant=aux;
          auxnovo->prox=NULL;
          return;
        }
        if(aux->prox!=NULL){
          auxnovo->prox=aux->prox;
          aux->prox->ant=auxnovo;
          auxnovo->ant=aux;
          aux->prox=auxnovo;
        return;
        } 
          aux=aux->prox;
        }  
      }

      if(aux->prox==NULL){ 

        if (compare < 0){
         auxnovo->prox=NULL;
         aux->prox=auxnovo;
         auxnovo->ant=aux;
         aux->ant=NULL;
         return;
        } 

        if (compare > 0){
         aux->prox=NULL;
         aux->ant=auxnovo;
         auxnovo->prox=aux;
         auxnovo->ant=NULL;
         return;
        }

      }  

      while(aux->prox!=NULL){
       
       if (compare < 0 && strcmp(aux->prox->nome, nome) > 0){ 
         auxnovo->prox=aux->prox;
         auxnovo->ant=aux;
         aux->prox->ant=auxnovo;
         aux->prox=auxnovo;
         return;
       }

      if (compare > 0){
         auxnovo->prox=aux;
         aux->ant=auxnovo;
         auxnovo->ant=NULL;
         (*inicio)=auxnovo;
         return;
      }

      if(compare < 0 && aux->prox->prox==NULL){
         auxnovo->prox=NULL;
         auxnovo->ant=aux->prox;
         aux->prox->ant=aux;
         aux->prox->prox=auxnovo;
         return;
      }

      aux=aux->prox;
      }
}

void searchName(struct cad *inicio){

  char nome[30];

  getNome(nome);

  char s = getStatus();

  struct cad *aux=inicio;

  while (aux!=NULL){


    if (strcmp(nome, aux->nome) == 0 && aux -> status == s){
      cout << "Encontramos " << aux->nome << ". Segue ficha:\n";
      cout << "ID: " << aux->id << "\n";
      cout << "Nome: " << aux->nome << "\n"; 
      cout << "idade: " << aux->idade << "\n";
      cout << "Sexo: " << aux->sexo << "\n";
      cout << "Status: " << (isAdopted(aux -> status) ? "Adotado" : "Não adotado") << "\n";
      cout << "Espécie: " << aux->especie << "\n";
      cout << "Raça: " << aux->raca << "\n";
      cout << "Características gerais: " << aux->carac << "\n";
      cout << "Data de cadastro: " << aux->data_cad << "\n";
      cout << "Data de alteração: " << aux->data_alt << "\n";
    
    }
    aux=aux->prox;
  }

  cout << "\nFim da Busca.\n";

}

void searchSpecies(struct cad *inicio){

  char especie[20];
  int qnt=0;

  getEspecie(especie);

  char s = getStatus();

  struct cad *aux=inicio;

  cout<< "\nListagem por espécie <" << especie << ">:\n";

  while (aux != NULL){

    if (strcmp(especie, aux->especie) == 0 && aux -> status == s){

      cout << "ID: " << aux->id << "\n";
      cout << "Nome: " << aux->nome << "\n"; 
      cout << "idade: " << aux->idade << "\n";
      cout << "Sexo: " << aux->sexo << "\n";
      cout << "Status: " << (isAdopted(aux -> status) ? "Adotado" : "Não adotado") << "\n";
      cout << "Raça: " << aux->raca << "\n";
      cout << "Características gerais: " << aux->carac << "\n";
      cout << "Data de cadastro: " << aux->data_cad << "\n";
      cout << "Data de alteração: " << aux->data_alt << "\n";
      

      qnt=qnt+1;

    } 
    aux=aux->prox;
  }

 cout << "\nForam encontrados " << qnt << " animais da espécie " << especie << ".\n";
}

void searchSpeciesAndBreed(struct cad *inicio){

  char especie[20], raca[20];

  getEspecie(especie);

  getRaca('N', NULL, raca);

  char s = getStatus();

  struct cad *aux=inicio;

  cout << "Animais da espécie " << especie << " e raça " << raca << ":\n";

  while (aux != NULL){

    if (strcmp(especie, aux->especie) == 0 && strcmp(raca, aux->raca) == 0 && aux -> status == s){

      cout << "ID: " << aux->id << "\n";
      cout << "Nome: " << aux->nome << "\n"; 
      cout << "idade: " << aux->idade << "\n";
      cout << "Sexo: " << aux->sexo << "\n";
      cout << "Status: " << (isAdopted(aux -> status) ? "Adotado" : "Não adotado") << "\n";
      cout << "Características gerais: " << aux->carac << "\n";
      cout << "Data de cadastro: " << aux->data_cad << "\n";
      cout << "Data de alteração: " << aux->data_alt << "\n";
    }
    aux=aux->prox;
  }

  cout << "Fim da listagem por Espécie e Raça.\n";

}

void searchSpeciesBreedAndSex(struct cad *inicio){

  char especie[20], raca[20], sexo;

  getEspecie(especie);

  getSexo(&sexo);

  getRaca(sexo, NULL, raca);

  char s = getStatus();

  struct cad *aux=inicio;

  cout << "Animais da espécie " << especie << ", raça " << raca << " e sexo " << sexo << ":\n";

  while (aux != NULL){

    if (strcmp(especie, aux -> especie) == 0 && strcmp(raca, aux->raca) == 0 && sexo == aux->sexo && aux -> status == s){

      cout << "ID: " << aux->id << "\n";
      cout << "Nome: " << aux->nome << "\n"; 
      cout << "idade: " << aux->idade << "\n";
      cout << "Sexo: " << aux->sexo << "\n";
      cout << "Status: " << (isAdopted(aux -> status) ? "Adotado" : "Não adotado") << "\n";
      cout << "Características gerais: " << aux->carac << "\n";
      cout << "Data de cadastro: " << aux->data_cad << "\n";
      cout << "Data de alteração: " << aux->data_alt << "\n";
      }
    aux=aux->prox;
  }

  cout << "Fim da listagem por Espécie, Raça e Sexo.\n";

}

void counting(struct cad *inicio){

  struct cad *aux=inicio;
  int qnt=0;

  while (aux != NULL){
    qnt=qnt+1;
    aux=aux->prox;
  }

  cout << "\nExistem " << qnt << " animais cadastrados no sistema.\n";

}

void countingOfBreed (struct cad *inicio){

  int qntcanino = 0; 
  int qntfelino = 0; 
  int qntroedor = 0; 
  int qntreptil = 0;
  int qntoutros = 0;
  struct cad *aux=inicio;


  while (aux != NULL){

    if (strcmp(aux->especie, "CANINO") == 0){
      qntcanino=qntcanino+1;
    }

    if (strcmp(aux->especie, "REPTIL") == 0){
      qntcanino=qntcanino+1;
    }

    if (strcmp(aux->especie, "FELINO") == 0){
      qntfelino=qntfelino+1;
    }

    if(strcmp(aux->especie, "ROEDOR") == 0){
      qntroedor=qntroedor+1;
    }

    if(strcmp(aux->especie, "CANINO") != 0 && strcmp(aux->especie, "FELINO") != 0 && strcmp(aux->especie, "ROEDOR") != 0 && strcmp(aux->especie, "RÉPTIL") != 0){
      qntoutros=qntoutros+1;
    }

   aux=aux->prox;

  }
 
  cout << "Quantidade de animais da espécie CANINA cadastrados: " << qntcanino << ".\n";
  cout << "Quantidade de animais da espécie FELINA cadastrados: " << qntfelino << ".\n";
  cout << "Quantidade de animais da espécie ROEDOR cadastrados: " << qntroedor << ".\n";
  cout << "Quantidade de animais da espécie RÉPTIL cadastrados: " << qntroedor << ".\n";
  cout << "Quantidade de animais de OUTRAS espécies cadastrados: " << qntoutros << ".\n";

}

void removeAnimal(struct cad **inicio) {
  char nome[30];
  int id, qnt=0, x;
  struct cad *aux=(*inicio);

  cout << "Digite o nome do animal que terá o cadastro DELETADO: ";
  cin.ignore();
  cin.getline(nome, 30);

  while(aux!=NULL){
    if(strcmp(nome, aux->nome) == 0){
      cout << "Encontramos " << aux->nome << ". Segue ficha:\n\n";

      cout << "ID: " << aux->id << "\n";
      cout << "Nome: " << aux->nome << "\n"; 
      cout << "idade: " << aux->idade << "\n";
      cout << "Sexo: " << aux->sexo << "\n";
      cout << "Status: " << (isAdopted(aux -> status) ? "Adotado" : "Não adotado") << "\n";
      cout << "Espécie: " << aux->especie << "\n";
      cout << "Raça: " << aux->raca << "\n";
      cout << "Características gerais: " << aux->carac << "\n\n";
      cout << "Data de cadastro: " << aux->data_cad << "\n";
      cout << "Data de alteração: " << aux->data_alt << "\n";

      id=aux->id;
      qnt++;
    }
    aux=aux->prox;
  }

  if (qnt == 0) {
    cout << "\n\nNão existe animal de nome " << nome << " cadastrado no sistema.\n\n";
    return;
  }

  if(qnt==1){
  cout << "\n\nEncontramos apenas um animal de nome " << nome << " para ser DELETADO.\n\n";
    
  aux=(*inicio);

  if(aux->prox==NULL){
        aux=NULL;
        (*inicio)=aux;
        cout << "\n\nO único elemento da lista foi apagado com sucesso!\n\n";
        return;
  }

  while (aux->prox->id != id){
    aux=aux->prox;
  }

  if(aux->prox->id == id){
    if(aux->prox->prox==NULL){
      aux->prox=NULL;
      return;
    }

    if(aux->prox->prox!=NULL){
      aux->prox=aux->prox->prox;
      aux->prox->prox->ant=aux;
      return;
    }
  }
}

if(qnt > 1) {
    cout << "Existem mais de um animal com o nome " << nome << " no sistema. Identifique-o pelo ID: ";
    cin >> id;

  aux=(*inicio);

  if(aux->id==id){
    aux->prox=(*inicio);
    return;
  }

  while (aux->prox->id != id){
    aux=aux->prox;
  }

  if(aux->prox->id == id){
    if(aux->prox->prox==NULL){
      aux->prox=NULL;
      return;
    }

    if(aux->prox->prox!=NULL){
      aux->prox=aux->prox->prox;
      return;
    }
  }
}
}

void changeAnimalStatus(struct cad **inicio) {
  char nome[30];
  int id, qnt=0, x;
  struct cad *aux=(*inicio);

  cout << "Digite o nome do animal que terá o status alterado: ";
  cin.ignore();
  cin.getline(nome, 30);

  while(aux!=NULL){
    if(strcmp(nome, aux->nome) == 0){
      cout << "Encontramos " << aux->nome << ". Segue ficha:\n\n";

      cout << "ID: " << aux->id << "\n";
      cout << "Nome: " << aux->nome << "\n"; 
      cout << "idade: " << aux->idade << "\n";
      cout << "Sexo: " << aux->sexo << "\n";
      cout << "Status: " << (isAdopted(aux -> status) ? "Adotado" : "Não adotado") << "\n";
      cout << "Espécie: " << aux->especie << "\n";
      cout << "Raça: " << aux->raca << "\n";
      cout << "Características gerais: " << aux->carac << "\n\n";
      cout << "Data de cadastro: " << aux->data_cad << "\n";
      cout << "Data de alteração: " << aux->data_alt << "\n";

      id=aux->id;
      qnt++;
    }
    aux=aux->prox;
  }

  if(qnt > 1) {
    cout << "Existem mais de um animal com o nome " << nome << " no sistema. Identifique-o pelo ID: ";
    cin >> id;
  }

  char s = getStatus();

  changeStatus(inicio, id, s);

}

void changeStatus(struct cad **inicio, int id, char newStatus) {
  struct cad *aux=(*inicio);

  while(aux!=NULL){
    if(aux -> id == id){
      aux -> status = newStatus;

      cout << "O status do animal " << aux -> nome << " foi alterado para: " << (isAdopted(aux -> status) ? "Adotado" : "Não adotado") << endl;
      return;

    }
  }
  cout << "Não foi encontrado nenhum animal com este ID." << endl;
}

void changeRegister(struct cad **inicio){

  char nome[30], especie[30], sexo, raca[20], carac[100];
  int id, qnt = 0, x;
  int idade;
  struct cad *aux=(*inicio);
  
  time_t atual;
  atual = time(NULL);

  cout << "Digite o nome do animal que terá o cadastro modificado: ";
  cin.ignore();
  cin.getline(nome, 30);

  while(aux!=NULL){
    if(strcmp(nome, aux->nome) == 0){
      cout << "Encontramos " << aux->nome << ". Segue ficha:\n";
      cout << "ID: " << aux->id << "\n";
      cout << "Nome: " << aux->nome << "\n"; 
      cout << "idade: " << aux->idade << "\n";
      cout << "Sexo: " << aux->sexo << "\n";
      cout << "Status: " << (isAdopted(aux -> status) ? "Adotado" : "Não adotado") << "\n";
      cout << "Espécie: " << aux->especie << "\n";
      cout << "Raça: " << aux->raca << "\n";
      cout << "Características gerais: " << aux->carac << "\n";
      cout << "Data de cadastro: " << aux->data_cad << "\n";
      
      id = aux -> id;
      qnt++;
    }
    aux=aux->prox;
  }

  if (qnt == 0) {
    cout << "Não existe animal de nome " << nome << " cadastrado no sistema.\n";
    return;
  }

  if(qnt > 1) {
    cout << "Existem mais de um animal com o nome " << nome << " no sistema. Identifique-o pelo ID: ";
    cin >> id;
  }

  cout << "ID -> " << id << endl;
  
  aux=(*inicio);

  do {
    aux = aux -> prox;
  }while(aux -> id != id);

  if (strcmp(nome, aux->nome) != 0) {
    cout << "O ID " << id << " não pertence ao animal descrito." << endl;
    return;
   }

    cout << "O que você deseja alterar?\n";
    cout << "1. Nome.\n";
    cout << "2. Espécie.\n";
    cout << "3. Sexo.\n";
    cout << "4. Raça.\n";
    cout << "5. Idade.\n";
    cout << "6. Características gerais.\n";
    cout << "7. Nada.\n";

    cin >> x;

    switch(x){
      case 1: 
      char nome[30], especie[30], raca[20];
      cout << "Qual o novo nome do animal?\n";
      cin.ignore();
      cin.getline(nome, 30);
      strcpy(aux->nome, nome);
      cout << "O nome do animal foi alterado para " << nome << endl;
      strcpy(aux -> data_alt, ctime(&atual));
      break;

      case 2: 
      cout << "Para qual espécie quer mudar?\n";
      cin.ignore();
      cin.getline(especie, 30);
      cout << "A espécie do animal foi alterada para " << especie << endl;
      strcpy(aux->especie, especie);
      strcpy(aux -> data_alt, ctime(&atual));
      break;

      case 3:
        char s;
        do {
          cout << "Qual é o sexo do animal? Escolha entre [F] e [M]:\n";
          cin >> s;
        }while(s != 'F' && s != 'M');
        aux -> sexo = s;
        strcpy(aux -> data_alt, ctime(&atual));
      break;

      case 4: 
      cout << "Para qual raça deseja mudar?\n";
      cin.ignore();
      cin.getline(raca, 20);
      cout << "A raça do animal foi alterada para " << raca << endl;
      strcpy(aux->raca, raca);
      strcpy(aux -> data_alt, ctime(&atual));
      break;

      case 5:
      cout << "Qual a nova idade do animal?\n";
      cin >> idade;
      cout << "A idade do animal foi alterada para " << idade << "\n";
      strcpy(aux -> data_alt, ctime(&atual));
      break;

      case 6: 
      cout << "Digite as novas características gerais do animal:\n";
      cin.ignore();
      cin.getline(carac, 100);
      strcpy(aux -> data_alt, ctime(&atual));
      break;

      case 7: 
      return;
    }
}