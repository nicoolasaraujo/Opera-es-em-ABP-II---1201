#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct no* arvbin;

struct no{
  int info;
  struct no* esq;
  struct no* dir;

};


arvbin *ciar_arvbin(){
  arvbin* raiz=(arvbin*)malloc(sizeof(arvbin));
  if(raiz!=NULL)
  *raiz=NULL;
  return raiz;
}


void libera_no(struct no* no){
  if(no==NULL){
    return;
  }
  libera_no(no->esq);
  libera_no(no->dir);
  free(no);
  no=NULL;
}

void libera_arvbin(arvbin* raiz){
  if(raiz==NULL){
    return;
  }
  libera_no(*raiz);
  free(raiz);
}

int vazia(arvbin *raiz){
  if(raiz==NULL){
    return 1;
  }
  if(*raiz==NULL)
  return 1;
  return 0;
}


int insere_arvbin(arvbin *raiz, int valor){
  if(raiz==NULL)
  return 0;
  struct no* novo;
  novo=(struct no*) malloc(sizeof(struct no));
  if(novo==NULL)
  return 0;
  novo->info=valor;
  novo->dir=NULL;
  novo->esq=NULL;
  if(*raiz==NULL){
    *raiz=novo;
  }else{
    struct no* atual= *raiz;
    struct no* ant=NULL;
    while(atual!=NULL){
      ant=atual;
      if(valor==atual->info){
        free(novo);
        return 0;
      }
      if(valor > atual->info)
      atual=atual->dir;
      else
      atual=atual->esq;
    }
    if(valor > ant->info)
    ant->dir=novo;
    else
    ant->esq=novo;
  }
  return 1;
}

void prefixa(arvbin* raiz, int *n){
  if(raiz==NULL){
    return;
  }
  if(*raiz!=NULL){
    if(*n==0){
        printf("%d",(*raiz)->info);
        *n=1;
    }else
        printf(" %d",(*raiz)->info );
    prefixa(&((*raiz)->esq),n);
    prefixa(&((*raiz)->dir),n);
  }
}


void infixa(arvbin *raiz, int *n){
  if(raiz==NULL)
  return;
  if(*raiz!=NULL){
    infixa(&((*raiz)->esq),n);
    if(*n==0){
        printf("%d",(*raiz)->info);
        *n=1;
    }else
        printf(" %d",(*raiz)->info );
    infixa(&((*raiz)->dir),n);
  }
}

void posfixa(arvbin * raiz, int *n){
  if(raiz==NULL)
  return;
  if(*raiz!=NULL){

    posfixa(&((*raiz)->esq),n);
    posfixa(&((*raiz)->dir),n);
    if(*n==0){
        printf("%d",(*raiz)->info);
        *n=1;
    }else
        printf(" %d",(*raiz)->info );
  }

}

struct no* remove_atual(struct no* atual){
  struct no *no1,*no2;
  if(atual->esq==NULL){
    no2=atual->dir;
    free(atual);
    return no2;
  }
  if(atual->dir==NULL){
    no2=atual->esq;
    free(atual);
    return no2;

  }
  no2=atual->esq;
  no1=atual;
  while(no2->dir!=NULL){
    no1=no2;
    no2=no2->dir;
  }
  if(no1!=atual){
    no1->dir=no2->esq;
    no2->esq = atual->esq;
  }
  no2->dir=atual->dir;
  free(atual);
  return no2;
}


int removearvbin(arvbin *raiz, int valor){
  if(raiz==NULL) return 0;
  struct no* ant=NULL;
  struct no* atual= *raiz;
  while(atual!=NULL){
    if(valor==atual->info){
      if(atual== *raiz)
        *raiz=remove_atual(atual);
      else{
        if(ant->dir==atual)
          ant->dir=remove_atual(atual);
        else
          ant->esq= remove_atual(atual);
      }
      return 1;
    }
    ant=atual;
    if(valor> atual->info)
      atual=atual->dir;
    else
      atual=atual->esq;
  }

}
int busca(arvbin *raiz,int valor){
  if(raiz==NULL){
    return 0;
  }
  if(*raiz!=NULL){
    struct no * atual=*raiz;
    while(atual!=NULL){
      if(atual->info==valor){
        return 1;
      }
      if(valor > atual->info){
        atual=atual->dir;
      }else{
        atual=atual->esq;
      }


    }
    return 0;
  }

}
void browser(arvbin *raiz, int valor){
  if(busca(raiz, valor)==1){
    printf("%d existe\n", valor);
  }else
  printf("%d nao existe\n", valor);


}


int main(){
  arvbin *raiz=ciar_arvbin();
  int valor,n;
  char teste[10];
  while(scanf("%s",teste)!=EOF){
  if(strcmp(teste,"I")==0){
    scanf("%d",&valor );
    insere_arvbin(raiz,valor);
  }else
    if(strcmp(teste,"INFIXA")==0){
      n=0;
      infixa(raiz,&n);
      if(*raiz!=NULL)
        printf("\n");
    }
  else if(strcmp(teste,"PREFIXA")==0){
    n=0;
    prefixa(raiz,&n);
    if(*raiz!=NULL)
      printf("\n");
  }else if(strcmp(teste,"POSFIXA")==0){
    n=0;
    posfixa(raiz,&n);
    if(*raiz!=NULL)
      printf("\n");
  }else if(strcmp(teste,"P")==0){
    scanf("%d",&valor);
    browser(raiz,valor);

  }
  else if(strcmp(teste,"R")==0){
    scanf("%d",&valor);
    removearvbin(raiz,valor);
  }
}



  return 0;
}
