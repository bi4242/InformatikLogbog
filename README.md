# Informatiklogbog
# Intro til programmering og vektorer

## Boldsimulation

<https://editor.p5js.org/jona117x/sketches/9WXB5jx9g>

## Simulation af faldende objekt

<https://editor.p5js.org/jona117x/sketches/AiVQf--uk>

## Tilfældige punkter …or is it? (Sierpinsky-trekant)

### Sketch

<https://editor.p5js.org/jona117x/sketches/6A8IyDlBl>

### Flowchart

![image](https://github.com/user-attachments/assets/23351fb7-4756-4ac2-917f-60e306fd9abb)


## Program-bytte med Elias

### Eget program

<https://editor.p5js.org/jona117x/sketches/6A8IyDlBl>

### Flowchart af Elias’ program

![image](https://github.com/user-attachments/assets/95e370a0-bf2f-49e5-9054-b129770dc955)


## LSD-radix-sortering

### Flowchart

![image](https://github.com/user-attachments/assets/b0cc90df-6298-4fb4-8994-aa907d90320b)


### Program (C#)

```
// See https://aka.ms/new-console-template for more information

namespace Test
{
    
    public static class Sort
    {
        const int Base = 4;
        public static void Main(string[] args)
        {
            int[] list = [4, 6, 81, 12, 2, 8];
            Console.WriteLine(String.Join(", ", list));
            SortList(list);
            Console.WriteLine(String.Join(", ", list));
        }
        public static void SortList(int[] list)
        {
            int digits = DigitsInLongestNumber(list);

            int[] auxiliary = new int[list.Length];

            for (int i = 0; i < digits; i++)
            {
                int[] digitCounts = CopyToAuxiliary(list, auxiliary, i);
                CopyFromAuxiliary(list, auxiliary, digitCounts, i);
            }
        }

        static int[] CopyToAuxiliary(int[] list, int[] auxiliary, int digit)
        {
            int[] digitCounts = new int[Base];

            for (int i = 0; i < list.Length; i++)
            {
                int number = list[i];

                int digitValue = GetDigit(number, digit);
                digitCounts[digitValue] += 1;

                auxiliary[i] = number;
            }

            return digitCounts;
        }

        static void CopyFromAuxiliary(int[] list, int[] auxiliary, int[] digitCounts, int digit)
        {
            int[] startPositions = digitCounts;
            for (int i = 0; i < startPositions.Length - 1; i++)
            {
                startPositions[i + 1] += startPositions[i];
            }
            for (int i = startPositions.Length - 1; i > 0; i--)
            {
                startPositions[i] = startPositions[i - 1];
            }
            startPositions[0] = 0;

            for (int i = 0; i < auxiliary.Length; i++)
            {
                int digitValue = GetDigit(auxiliary[i], digit);
                list[startPositions[digitValue]] = auxiliary[i];
                startPositions[digitValue] += 1;
            }
        }

        static int DigitsInLongestNumber(int[] list)
        {
            int longest = 1;
            foreach (int num in list)
            {
                int d = 1;
                int number = num;
                while (number >= Base)
                {
                    number /= Base;
                    d++;
                }
                longest = Math.Max(longest, d);
            }
            return longest;
        }

        static int GetDigit(int number, int digit)
        {
            return (int)(number / Math.Pow(Base, digit) % Base);
        }
    }
}
```

# Kryptering

## Cæsar-/Vigenerekode

<https://editor.p5js.org/jona117x/sketches/Bi2gz4rrb>

# 3D-modellering og makerspace

## Onshape-modeller af geometriske figurer med heltalligt rumfang

<https://cad.onshape.com/documents/a7a5156378c0f82def0293cb/w/bdbbb1b3a0da9c8feb42491c/e/d9d4cc36ae927f4d42d44b89>

# Arduino

## Simuleret kontinuerlig lysstyrke i diode med binært input

```
#define JOY_Y A2
const int SCALE = 10000 / 1024;

void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
}

int lightLevel = 1000;

void loop() {
  digitalWrite(LED_BUILTIN, HIGH);
  delayMicroseconds(lightLevel);
  digitalWrite(LED_BUILTIN, LOW);
  
  lightLevel = analogRead(JOY_Y) * SCALE;
  lightLevel = (lightLevel + 50) % 10000;
  delayMicroseconds(10000 - micros() % 10000);
}
```
