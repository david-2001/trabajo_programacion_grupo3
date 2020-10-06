# trabajo_programacion_grupo3
#include<stdio.h>
#include<stdlib.h>
#include<time.h>
#include "tala.h"

void menuPrincipal();
void terrenoManual();
void terrenoPredeterminado();
void salir();
int ingreseOpcion();
float volMaderaExtraer();
void resultado(float vol_madera_bosque);
void ingresoDiametro(float diametro[][100]);
void ingresoAltura(float altura[][100]);
void imprimirDiametro(float diametro[][100]);
void imprimirAltura(float altura[][100]);
void diametro_aleatorio(float randomDiametro[][50]);
void altura_aleatorio(float randomAltura[][50]);
void archivoAltura();
void archivoDiametro();

float suma_diametro = 0;
float suma_altura = 0;
	
int filas, columnas;


int main(){
	
menuPrincipal();
	while(1){
	switch(ingreseOpcion()){
	
	case 1 : terrenoManual();           
		return 0;

	case 2 : terrenoPredeterminado();
		return 0;
	
	case 3: archivoAltura();
			printf("\n");
			archivoDiametro();
		return 0;
	
	case 4: salir();
		return 0;
		
	default: printf("a ingresado una opcion invalida, por favor ingrese una opcion nuevamente:\n");
	
	}

}
	return 0;
	
}

int ingreseOpcion(){
	int opcion;
	scanf("%d", &opcion);		
	return opcion;
	}
	
void menuPrincipal(){
	
	printf("*--------------------------------*\n");
	printf("*-------elija una opcion---------*\n");
	printf("*--------------------------------*\n");
	printf("1.- ingresar terreno manualmente\n");
	printf("2.- utilizar un terreno aleatorio\n");
	printf("3.- acceder a un terreno predeterminado\n");
	printf("4.- salir\n");
	printf("\n");
}
	
void terrenoManual(){
	float vol_madera_bosque;
	float diametro[100][100]; 
	float altura[100][100];  
	float promedio_diametro;
	float promedio_altura;

	printf("-------diametro del tronco--------\n");
	printf("\n");
	
	printf("digite el numero de filas: ");
	scanf("%d", &filas);
	printf("digite el numero de columnas: ");
	scanf("%d",&columnas);
	
	ingresoDiametro(diametro);
		
	imprimirDiametro(diametro);
	
	printf("\n");
	printf("----altura de los arboles------\n");
	
	ingresoAltura(altura);
	imprimirAltura(altura);
	
	promedio_altura = (suma_altura)/(filas*columnas);
	promedio_diametro = (suma_diametro)/(filas*columnas); 
	vol_madera_bosque= promedio_diametro*promedio_altura*(filas*columnas)/10000*filas*columnas;

	
	resultado(vol_madera_bosque);
}

void terrenoPredeterminado(){
	float vol_madera_bosque;
	float randomDiametro[50][50];
	float randomAltura[50][50];
	float promedio_diametro;
	float promedio_altura;
	int filas = 50, columnas = 50;

	diametro_aleatorio(randomDiametro);
	altura_aleatorio(randomAltura);
	
	promedio_diametro = (suma_diametro)/(filas*columnas); 
	promedio_altura = (suma_altura)/(filas*columnas);
	vol_madera_bosque= promedio_diametro*promedio_altura*(filas*columnas)/(10000)*(filas*columnas);
	
	resultado(vol_madera_bosque);
	}

void salir(){
	printf("usted ha salido del programa");
}

void ingresoDiametro(float diametro[][100]){
		
		printf("\nnota: solo se permiten valores del 0 al 4\n");
	
	for(int i = 0; i < filas; i++){
		for(int j = 0; j < columnas; j++){
		
			printf("\ndigite el diametro de cada arbol en metros en la posicion [%d][%d]: ", i+1, j+1 );
			scanf("%f", &diametro[i][j]);
			
			while((diametro[i][j]) < 0 || (diametro[i][j]) > 4){
			printf("\nvalor invalido, ingrese el diametro en metros nuevamente\n");
			printf("\ndigite el diametro de cada arbol en metros en la posicion [%d][%d]: ", i+1, j+1 );
			scanf("%f", &diametro[i][j]);
		}
		suma_diametro += diametro[i][j];
		printf("\n");
		}
	}
	
}

void ingresoAltura(float altura[][100]){
	
	printf("\nnota: solo se permiten valores del 0 al 60\n");
		
	for(int i = 0; i < filas; i++){
		for(int j=0; j < columnas; j++){

			printf("\ndigite la altura en metros de cada arbol en la posicion [%d][%d]: ", i+1, j+1 );
			scanf("%f", &altura[i][j]);
			
			while((altura[i][j]) < 0 || (altura[i][j]) > 60){
			printf("\nvalor invalido, ingrese el diametro en metros nuevamente\n");
			printf("\ndigite la altura de cada arbol en metros en la posicion [%d][%d]: ", i+1, j+1 );
			scanf("%f", &altura[i][j]);
		}
			suma_altura+= altura[i][j];
			printf("\n");
			
		}
	}
	
}

void imprimirDiametro(float diametro[][100]){
	for(int i = 0; i < filas; i++){
		for(int j = 0; j < columnas; j++){
		printf("[%.2f]", diametro[i][j]);
				}
		printf("\n");	
	}
	
}
void imprimirAltura(float altura[][100]){
	for(int i = 0; i < filas; i++){
		for(int j = 0; j < columnas; j++){
			printf("[%.2f]", altura[i][j]);
		}
		printf("\n");
	}
	
}

void diametro_aleatorio(float randomDiametro[][50]){
	
	time_t t;
	srand((unsigned) time(&t));
	int filas = 50, columnas = 50;

	for(int i = 0; i < filas; i++ ){
		for(int j = 0; j < columnas; j++){
		  
		randomDiametro[i][j] = rand() % 2;
		suma_diametro += randomDiametro[i][j];
		}
	}
	
}

void altura_aleatorio(float randomAltura[][50]){
	
	time_t t;
	srand((unsigned) time(&t));
	int filas = 50, columnas = 50;
	
	for(int i = 0; i < filas; i++ ){
		for(int j = 0; j < columnas; j++){
		  
		randomAltura[i][j] = rand() % 21 ; 
		suma_altura+= randomAltura[i][j];
		}
	}
}

float volMaderaExtraer(){
	float vol_madera_extraer;
	
	printf("ingrese el volumen de madera en metros cubicos que desea extraer: \n");
	scanf("%f", &vol_madera_extraer);
	while(vol_madera_extraer < 0){
		printf("valor invalido, por favor ingrese valores mayores a 0\n");
		printf("\ningrese el volumen de madera en metros cubicos que desea extraer: \n");
		scanf("%f", &vol_madera_extraer);
		}
	return vol_madera_extraer;
}

void resultado( float vol_madera_bosque){
	
	if(vol_madera_bosque > volMaderaExtraer()){
	printf("se ha realizado una tala controlada en el sector\n");
	}else{ 
	printf("no se ha realizado una tala controlada en el sector\n");
	}
}
void archivoAltura(){
	FILE* archivo = fopen("altura.txt", "r");
	
	char alturaArch[100];
	char filasColumnas[10];
	char titulo1[25];
	int cant_num = 0;
	
	fscanf(archivo,"%s", filasColumnas);
	printf("%s\n", filasColumnas);
	printf("\n");
	
	fscanf(archivo,"%s\n", titulo1);
	printf("%s\n", titulo1);
	printf("\n");
	
	while(fscanf(archivo,"%s", alturaArch) == 1){
		cant_num++;
		printf("%s\n", alturaArch);
	}
	
	fclose(archivo);	
}

void archivoDiametro(){
	FILE* archivo = fopen("diametro.txt", "r");
	
	char diametroArch[100];
	char filasColumnas[10];
	char titulo2[25];
	int cant_num = 0;
	
	fscanf(archivo,"%s", filasColumnas);
	printf("%s\n", filasColumnas);
	printf("\n");
	
	fscanf(archivo,"%s\n", titulo2);
	printf("%s\n", titulo2);
	printf("\n");
	
	while(fscanf(archivo,"%s", diametroArch) == 1){
		cant_num++;
		printf("%s\n", diametroArch);
	}
	
	fclose(archivo);
	
}
