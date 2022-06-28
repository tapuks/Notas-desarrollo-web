# Notas-desarrollo-web

export class AppComponent {
  @ViewChild("dado1",null) dado1: DadoComponent | undefined;
  title = 'dados';
  number1=0
  number2=0
  number3=0
  // @Output() envioNumeros:EventEmitter<number[]>;
 

  constructor(){
    // this.envioNumeros= new EventEmitter()
  }
  



generateNumbers(){
  // this.number1 = Math.floor(Math.random() * (6 - 1 + 1) + 1);
  this.number2 = Math.floor(Math.random() * (6 - 1 + 1) + 1);
  this.number3 = Math.floor(Math.random() * (6 - 1 + 1) + 1);
  this.dado1.tirar()


}


//DADO COMPONENT
tirar(){
    this.numero = Math.floor(Math.random() * (6 - 1 + 1) + 1);
  }
  
 // HTML DEL APP
 <app-dado #dado1></app-dado>
  <app-dado [numero]="number2"></app-dado>
  _________________________________________________
  VIEWCHILD (CON ESTO ACCEDEMOS A LOS METODOS DE OTRO COMPONENTE)
  1-EN EL APP.HTML
  <app-caja #caja></app-caja>
  2-CAJA.TS
   hola(){
    console.log('holaa');
  }
  3-APP.TS
  @ViewChild("caja",null) caja: CajaComponent | undefined;
  saludo(){
    this.caja.hola()
  }
  
  
  
  
 ____________________________________________________________
 HACER PETICIONES
 importtamos en el app.module.ts
 import { HttpClientModule } from '@angular/common/http';


y en el ts donde lo vayamosa utilizar importamos:
import {HttpClient} from '@angular/common/http'
 constructor(public http: HttpClient){

  }

  getDatos(){
      this.http.get("https://scratchya.com.ar/vue/datos.php").subscribe(
    (datos)=> {console.log('datos recibidos:' + datos);
                this.data= datos},
    (error)=> (console.log('error:' + error)));
  }
  
  //PODEMOS HACERLO CON UNA ENTIDAD (ENTITIES/ELEMENTO.TS)
  export class Elemento {
    codigo: string;
    descripcion: string;
    precio: string;

    constructor(){
        this.codigo = '';
        this.descripcion= '';
        this.precio = '';
    }
}

//EN EL TS
import { Elemento } from './entities/elemento';
data:Elemento[]=[];
  constructor(public http: HttpClient){
  }
  
 getDatos(){
    try{
    this.http.get<Elemento[]>("https://scratchya.com.ar/vue/datos.php").subscribe(
    (datos:Elemento[])=> {console.log('datos recibidos:' + datos);
                this.data= datos},
    (error)=> (console.log('error:' + error)));
    }
    catch (error){
    }
  }
  
//LA FORMA BUENA ES CREAR UN SERVICIO.
1-ng g s webService
2- En el web service:
 data:Elemento[]=[];

  constructor(public http: HttpClient) { 

  }

   getDatos(){
    try{
    this.http.get<Elemento[]>("https://scratchya.com.ar/vue/datos.php").subscribe(
    (datos:Elemento[])=> {console.log('datos recibidos:' + datos);
                this.data= datos},
    (error)=> (console.log('error:' + error)));
    }
    catch (error){
    }
  }
  
 3- en el app.ts
 import { WebServiceService } from './web-service.service';
constructor(public ws: WebServiceService){
 }
 
4- en el html ahora llamaremos al nombre dervicio con ws delante, que es el nombre que le hemos puesto en el constructor. Por ejemplo:
<p>ws.data.nombre</p>
 
 ________________________________________
 ESTO ES UNA PY
 <p>{{nombre | json}}</p>
 para crear uno propio que transforme numeros a ingles:
 1. ng g p letras
2. En letras pipe.ts

import { Pipe, PipeTransform } from '@angular/core';
@Pipe({
  name: 'letras'
})
export class LetrasPipe implements PipeTransform {
  transform(value: any, ...args: any[]): any {
    switch (value){
      case 1: return 'one'
      case 2: return 'two'
      case 3: return 'three'
      case 4: return 'four'
      case 5: return 'five'
      default:
        return ''
    }}} 
  3. en el html
  <p>{{4 | letras}}</p>
 
 
 
 



