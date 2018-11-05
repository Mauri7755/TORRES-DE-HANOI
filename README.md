# TORRES-DE-HANOI
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Hanoi
{
    class Program
    {

        static void Main(string[] args)
        {
          
            Console.WriteLine("TORRES DE HANOI");
         
            Console.Write("INGRESA UN NUMERO : ");
            Disco = int.Parse(Console.ReadLine());
            
           
            Console.WriteLine("");

            Console.CursorVisible = false;

            Max = (int)Math.Pow(2, Disco) - 1;

            for (int i = 0; i < 3 * Disco; i++)
            {
                ListaDiscos.Add(0);
            }

            for (int i = 0; i < Disco; i++)
            {
                ListaDiscos[0 + 3 * i] = (byte)(i + 1);
            }

          
            {
                Proceso = false;
                ArrayHanoi = new List<byte>();
                for (int i = 0; i < (Max + 1) * 3 * Disco; i++)
                {
                    ArrayHanoi.Add(0);
                }
                Console.Clear();  
                
                Console.WriteLine("IZQUERDA [A] Y DERECHA [S] ");
            }

            if (!Proceso)
            {
                Program.Tomar(0);
            }
            Program.THanoi(Disco, 0, 1, 2, ref Min);
            ConsoleKeyInfo keyboard;
            int aux = 0;
            if (!Proceso)
            {
                do
                {

                    DibujarHanoi(8, 3, aux);
                    keyboard = Console.ReadKey();
                    if (keyboard.Key == ConsoleKey.S)
                    {
                        if (aux + 1 < Max + 1)
                        {
                            aux++;
                        }
                    }
                    else if (keyboard.Key == ConsoleKey.A)
                    {
                        if (aux - 1 >= 0)
                        {
                            aux--;
                        }
                    }
                }
                while (keyboard.Key != ConsoleKey.Escape);

            }
            else
            {
                Console.ReadLine();
            }

        }
        static public List<byte> ListaDiscos = new List<byte>(); 
        static public List<byte> ArrayHanoi;

        static int Disco = 0; 
        static int Min = -1; 
        static int Max = 0; 
        static bool Proceso = false;

        public static void THanoi(int Disco, int Fuente, int T, int Destino, ref int i)
        {
            if (Disco > 0) 
            {

                THanoi(Disco - 1, Fuente, Destino, T, ref i);
                Movimiento(Disco, Fuente, Destino);

                
                if (Proceso)
                {
                    Array(8, 3);
                }
                else
                {
                    Tomar(i + 2);
                }
                i++;
                THanoi(Disco - 1, T, Fuente, Destino, ref i);
            }
        }

        public static void Movimiento(int Disco, int Fuente, int Destino)
        {
            ListaDiscos[Destino + 3 * (Disco - 1)] = ListaDiscos[Fuente + 3 * (Disco - 1)];
            ListaDiscos[Fuente + 3 * (Disco - 1)] = 0;
        }

        public static void Array(int X, int X2)
        {
            Console.WriteLine("");
            for (int i = 0; i < Disco; i++)
            {
                for (int f = 0; f < 3; f++)
                {
                    Console.SetCursorPosition(f * 3 + X, i + X2);
                    if (ListaDiscos[f + 3 * i] == 0) 
                    {
                        Console.Write(':');
                    }
                    else if (ListaDiscos[f + 3 * i] < 10)
                    {
                        Console.Write(ListaDiscos[f + 3 * i]);
                    }
                    else if (ListaDiscos[f + 3 * i] >= 10)
                    {
                        Console.Write((char)(ListaDiscos[f + 3 * i] + 55));
                    }
                }
            }

        }

        public static void Tomar(int i)
        {
            for (int j = 0; j < Disco; j++)
            {
                for (int f = 0; f < 3; f++)
                {
                    ArrayHanoi[(f + 3 * j) + (i * (Disco * 3))] = ListaDiscos[f + 3 * j];
                }
            }
        }

        public static void DibujarHanoi(int X, int X2, int i)
        {
            Console.WriteLine("");
            for (int j = 0; j < Disco; j++)
            {
                for (int f = 0; f < 3; f++)
                {
                    Console.SetCursorPosition(f * 3 + X, j + X2);
                    if (ArrayHanoi[(f + 3 * j) + (i * (Disco * 3))] == 0)
                    {
                        Console.Write(':');
                    }
                    else if (ArrayHanoi[(f + 3 * j) + (i * (Disco * 3))] < 10)
                    {
                        Console.Write(ArrayHanoi[(f + 3 * j) + (i * (Disco * 3))]);
                    }
                    else if (ArrayHanoi[(f + 3 * j) + (i * (Disco * 3))] >= 10)
                    {
                        Console.Write((char)(ArrayHanoi[(f + 3 * j) + (i * (Disco * 3))] + 55));
                    }
                }
            }
            Console.WriteLine("");
            Console.SetCursorPosition(X - 2, 1 + X2 + Disco);

        }
    }
}
