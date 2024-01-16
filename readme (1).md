# Lern-Periode 3

Max Muster

9.1.2024 bis 30.1.2024 (☃️ Sportferien)

## Grob-Planung

1. Wo stehen Sie mit Ihren Noten? In welchen Modulen waren Sie besonders stark; in welchen sind die ungenügend? Welche davon sind besonders wichtig.
   In Modul 164 habe ich eine Note von 2,5 erhalten, ich enpfand es sehr schwierig. Aber bei den Modulen 319 und 431 jeweils eine gute Note von 5 erreicht, wobei diese beiden        Module besonders      wichtig für meinen Studiengang sind.
   
3. Was hatten Sie sich am Ende von LP2 vorgenommen? Was war Ihr VBV? Wie könnten Sie diesen besonders gut üben?
   Wir habe Mehrheitlich an unserem Projekt gearbeitet und ich habe gelernt das man viel Zeit für ein Programm braucht und konzentriert seon muss damit nichts falsch geht.
   
5. Was wäre ein geeignetes Projekt würd diese LP3?
Ich werde etwas neues asprobieren und werde ein klienes spiel programmieren. ich denk so ein snake spiel.
   

## 9.1.2024

Heute habe ich während diese 4 Stunden alle meine Projekte durchgeschaut und habe paar interessante gefunde und habe mich entschieden mal etwas anderes zu programmieren und will ein Snake spiel programmieren. Während ich alle meine Projekte durchgeschaut habe, habe ich gemerkt das ich relativ viel gelernt habe und das ich viel mehr kann als in LP2 und bin Motiviert weiter zu machen.

## 16.1 und 23.1.2024

- [X] Es soll ein quadrat abgebildet werden in dem sich die Schalnge frei bewegen kann.
- [X] Die Schalnge soll sich in mindestens eine Richtung bewegen können.
- [X] Die Schlange soll sich frei in jede Richtung bewegen können.
- [X] Es sollen Äpfel erscheinen.

| estfall-Nummer | Ausgangslage (Given) | Eingabe (When) | Ausgabe (Then) | Erfüllt? |
| -------------- | -------------------- | -------------- | -------------- | -------- |
| 1               |                      |                |                |          |
| ...            |                      |                |                |          |
| 4              |                      |                |                |          |

✍️ Heute denke ich habe gut gearbeitet und bi sehr weit gekommen. Ich habe es aber noch nicht geschafft das eine SChnecke und ein Apfle abgebildet wird, sonst habe ich relativ konzentriert gearbeitet und hatte auch spass daran.

namespace SnakeGame
{
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading;

    class SnakeGame
    {
        static int width = 20;
        static int height = 10;
        static Queue<Position> snake = new Queue<Position>();
        static Position direction = new Position(1, 0);
        static Position food = new Position(0, 0);
        static bool isGameOver = false;

        static void Main()
        {
            Console.WindowHeight = height + 1;
            Console.WindowWidth = width + 1;
            Console.BufferHeight = Console.WindowHeight;
            Console.BufferWidth = Console.WindowWidth;

            InitializeGame();

            while (!isGameOver)
            {
                if (Console.KeyAvailable)
                    ProcessKey(Console.ReadKey(true).Key);

                MoveSnake();
                CheckCollision();
                CheckFood();

                if (isGameOver)
                    Console.WriteLine("Game Over!");

                Thread.Sleep(100);
            }
        }

        static void InitializeGame()
        {
            snake.Enqueue(new Position(0, 0));
            GenerateFood();
        }

        static void Draw()
        {
            Console.Clear();

            foreach (var position in snake)
                DrawAtPosition(position, 'O');

            DrawAtPosition(food, 'X');
        }

        static void DrawAtPosition(Position position, char symbol)
        {
            Console.SetCursorPosition(position.X, position.Y);
            Console.Write(symbol);
        }

        static void ProcessKey(ConsoleKey key)
        {
            switch (key)
            {
                case ConsoleKey.UpArrow:
                    direction = new Position(0, -1);
                    break;
                case ConsoleKey.DownArrow:
                    direction = new Position(0, 1);
                    break;
                case ConsoleKey.LeftArrow:
                    direction = new Position(-1, 0);
                    break;
                case ConsoleKey.RightArrow:
                    direction = new Position(1, 0);
                    break;
            }
        }

        static void MoveSnake()
        {
            Position head = snake.Last();
            Position newHead = new Position(head.X + direction.X, head.Y + direction.Y);

            if (newHead.X < 0)
                newHead.X = width - 1;
            else if (newHead.X >= width)
                newHead.X = 0;

            if (newHead.Y < 0)
                newHead.Y = height - 1;
            else if (newHead.Y >= height)
                newHead.Y = 0;

            snake.Enqueue(newHead);

            if (snake.Count > 1)
                DrawAtPosition(snake.Dequeue(), ' ');

            Draw();
        }

        static void CheckCollision()
        {
            Position head = snake.Last();

            if (snake.Count > 1 && snake.Take(snake.Count - 1).Any(p => p.Equals(head)))
                isGameOver = true;
        }

        static void GenerateFood()
        {
            Random random = new Random();
            food = new Position(random.Next(width), random.Next(height));

            while (snake.Contains(food))
                food = new Position(random.Next(width), random.Next(height));
        }

        static void CheckFood()
        {
            Position head = snake.Last();

            if (head.Equals(food))
            {
                GenerateFood();
            }
        }
    }

    class Position
    {
        public int X { get; set; }
        public int Y { get; set; }

        public Position(int x, int y)
        {
            X = x;
            Y = y;
        }

        public bool Equals(Position other)
        {
            return X == other.X && Y == other.Y;
        }
    }

}

## 23.1.2024

- [ ] Die Schalnge soll fähig sein Äpfel essen zu können.
- [ ] Jedes mal wenn die Schlange ein A isst soll er etwas länger werden.
- [ ] Und jedes mal wenn die Schlange ein Apfel isst soll nach paar SEkunden wider ein Apfel erscheinen.
- [ ] Punkte soll am schluss vom spiel gezeigt werden.

| Testfall-Nummer | Ausgangslage (Given) | Eingabe (When) | Ausgabe (Then) | Erfüllt? |
| --------------- | -------------------- | -------------- | -------------- | -------- |
| 5               |                      |                |                |          |
| ...             |                      |                |                |          |
| 8               |                      |                |                |          |

✍️ Heute am 23.1 habe ich... (50-100 Wörter)

☝️ Vergessen Sie nicht, bis zum 23.1 Ihren fixfertigen Code auf github hochzuladen, und in der Spalte **Erfüllt?** einzutragen, ob Ihr Code die Test-Fälle erfüllt

## 30.1.2024

✍️ Heute am 23.1 habe ich... (50-100 Wörter)

## Reflexion

Formen Sie Ihre Zusammenfassungen in Hinblick auf Ihren VBV zu einem zusammenhängenden Text von 100 bis 200 Wörtern (wieder mit Angabe in Klammern).

Verfassen Sie zusätzlich einen kurzen Abschnitt, in welchem Sie über die Länge der Projekte reflektieren: Fanden Sie die 9-wöchtige LP2 oder die 4-wöchige LP3 angenehmer? Was bedeutet das für Ihre Planung der zukünftigen LP?
