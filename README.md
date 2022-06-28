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
