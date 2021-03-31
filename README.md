# dio.bank
projeto de transferencia bancaria
using System;
using System.Collections.Generic;

namespace dio.bank
{
    class Program
    {

        static List<conta>  listacontas = new List<conta>{};
         static void Main(string[] args)
        {
           string opcaousuario = obteropcaousuario();

            while (opcaousuario.ToUpper() != "x")
            {

                switch (opcaousuario)
                {
                    case "1":  
                       // listarcontas{};
                         break;

                     case "2":
                        //inserircontas{};
                          break;

                     case "3":
                        // transferir{};
                          break;
                    
                     case "4":
                        sacar{};
                         break;

                     case "5":
                       // depositar{};
                        break;

                     case "c":
                         Console.Clear();
                         break;

                  default:
                     throw new  ArgumentOutOfRangeException{};
                }

                opcaousuario = obteropcaousuario();
            }

            Console.WriteLine("obrigado por utilizar nossos serviços.");
            Console.ReadLine();
        }
   
         
         private  static void  sacar()
          {
              Console.Write("digite o numero da conta:");
              int indiceconta = int.Parse(Console.ReadLine());

              Console.Write("digite o valor a ser sacado:");
              double valorsaque = double.Parse(Console.ReadLine());

              listacontas[indiceconta].sacar(valorsaque);

          }


         private static void inserirconta()
         {
            Console.WriteLine("inserir nova conta");

            Console.WriteLine("digite 1 para conta fisica ou 2 para juridica: ");
            int entradatipoconta = int.Parse(Console.ReadLine());

            Console.WriteLine("digite o nome do cliente : ");
            string entradanome = Console.ReadLine();

            Console.WriteLine("digite o saldo inicial: ");
            double entradasaldo = double.Parse(Console.ReadLine());

            Console.WriteLine("digite o credito: ");
            double entradacredito = double.Parse(Console.ReadLine());

            conta novaconta = new conta(tipoconta: (tipoconta)entradatipoconta,
                                       saldo: entradasaldo,
                                       credito: entradacredito,
                                       nome: entradanome);

            listacontas.Add(novaconta);


         }

         private static void listarcontas()
         {
              Console.WriteLine("listar contas");

              if (listacontas.Count == 0)
              {
                  Console.WriteLine("nenhuma conta cadastrada.");
                  return;
              }

              for (int i = 0; i < listacontas.Count; i++)
              {
                  conta conta = listacontas[i];
                  Console.Write("#{0} - ", i);
                  Console.WriteLine(conta);
              }

            }

        private static string obteropcaousuario()
        {

          Console.WriteLine();
          Console.WriteLine(" dio bank a seu dispor !!!");
          Console.WriteLine("informe a opcao desejada");

          Console.WriteLine("1- listar contas");
          Console.WriteLine("2- inserir nova conta");
          Console.WriteLine("3-transferir");
          Console.WriteLine("4- sacar");
          Console.WriteLine("5- depostar");
          Console.WriteLine("c- limpar a tela");
          Console.WriteLine("x- sai");
          Console.WriteLine();

          string opcaousuario = Console.ReadLine().ToUpper();
          Console.WriteLine();
          return opcaousuario;
    }

  }

}

using System;

namespace dio.bank
{
    public class conta
    {
        private tipoconta tipoconta {get; set;}

        private double saldo { get; set; }

        private double credito { get; set; } 

        private string nome { get; set;}

        public conta(tipoconta tipoconta, double saldo, double credito, string nome)
        {
          this.tipoconta = tipoconta;
          this.saldo = saldo;
          this.credito = credito;
          this.nome = nome;
        }

        
        public bool sacar(double valorsaque)
        {
            // validacao de saldo suficiente
            if (this.saldo - valorsaque < (this.credito *-1)){
            Console.WriteLine("saldo insuficiente");
            return false;

          }
      
            this.saldo -= valorsaque;
      
           Console.WriteLine("saldo atual da conta de {0} e {1}", this.nome, this.saldo);
           // htpps://docs.microsoft.com/pt-br/dotnet/standard/base-types/composite-formatting
          
           return true;

        }
    

         public void depositar(double valordeposito)
         {
             this.saldo += valordeposito;

             Console.WriteLine("saldo atual da conta de {0} e {1}", this.nome, this.saldo);
        }
     
        
         public void transferir(double valortransferencia, conta contadestino)
        {
            if (this.sacar(valortransferencia)){
                contadestino.depositar(valortransferencia);
            }
         
         
          }

        public override string ToString()
        {
           string retorno = "";
           retorno += "tipoconta " + this.tipoconta + "|";
           retorno += "nome " + this.nome + "|";
           retorno += "saldo " + this.saldo + "|";
           retorno += "credito" + this.credito + "|";
           return retorno;
        }
        
        

namespace dio.bank
{
  public  enum tipoconta
  {
     pessoafisica = 1,
     pessoajuridica = 2
 
  }

}


