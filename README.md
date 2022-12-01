# LR17
Грибов И.С

ЭВТ-70

Игровой Движок: Unity.

Лабораторная работа №17

Тема: Разработка игры Puzzle Plumber

Цель: разработать игру Puzzle Plumber

1. Создание папок Scenes, Scripts и Sprites

___________________![image](https://user-images.githubusercontent.com/119228138/204898861-dd09210d-cbe3-4fc7-ac93-f4bae6075402.png)

 ___________________Рис. 17.1 Папки Scenes, Scripts и Sprites

2. Объект Main Camera

___________________![image](https://user-images.githubusercontent.com/119228138/204898891-b4a484f1-852f-4c7a-b63e-4d697d556148.png)


 ___________________Рис. 17.2 Настройки объекта Main Camera

3. Объект grid и его дочерний объект BackTile_06

 ___________________![image](https://user-images.githubusercontent.com/119228138/204898913-a449b8c4-145b-46e4-ae09-454cd73643bf.png)


 ___________________Рис. 17.3 Настройка объекта grid

 ___________________![image](https://user-images.githubusercontent.com/119228138/204898947-a270c284-cf8e-47d4-b203-c5e0ffea176c.png)

 
 ___________________Рис. 17.4 Настройка объекта BackTile_06

4. Объект pipes и его дочерние объекты pipeGreen_10

 ___________________![image](https://user-images.githubusercontent.com/119228138/204898963-3dc27cea-1641-4ee0-bb06-c771e38be60e.png)


 ___________________Рис. 17.5 Настройка объекта pipes

 ___________________![image](https://user-images.githubusercontent.com/119228138/204898997-95d9881c-f87f-453b-8d68-83324f09ba0d.png)


 ___________________Рис. 17.6 Настройка объекта pipeGreen_10

5. Объект pipeGreen_22

___________________![image](https://user-images.githubusercontent.com/119228138/204899015-dd5ca063-54b2-4519-b757-5b52ce42ef84.png)


 ___________________Рис. 17.7 Настройка объекта pipeGreen_22

6. Объект pipeGreen_05

___________________![image](https://user-images.githubusercontent.com/119228138/204899063-c14ab645-9b0f-4800-ab24-83b9d9105ed4.png)


 ___________________Рис. 17.8 Настройка объекта pipeGreen_05

7. Объект GameManager

___________________![image](https://user-images.githubusercontent.com/119228138/204899089-d75bc8a6-7e76-497b-88a9-15dae8d4c2ba.png)


 ___________________Рис. 17.9 Настройка объекта GameManager

```
8.	Скрипт GameManager
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class GameManager : MonoBehaviour
{
    public GameObject PipesHolder;
    public GameObject[] Pipes;

    [SerializeField]
    int totalPipes = 0;
    [SerializeField]

    int correctPipes = 0;

    void Start()
    {
        totalPipes = PipesHolder.transform.childCount;

        Pipes = new GameObject[totalPipes];

        for (int i = 0; i < Pipes.Length; i++)
        {
            Pipes[i] = PipesHolder.transform.GetChild(i).gameObject;
        }
    }

   public void correctMove()
    {
        correctPipes += 1;

        Debug.Log("correct Move");

        if(correctPipes == totalPipes)
        {
            Debug.Log("You win!");
        }
    }

    public void wrongMove()
    {
        correctPipes -= 1;
    }
    
}

9.	Скрипт PipeScript
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
public class PipeScript : MonoBehaviour
{
    float[] rotations = { 0, 90, 180, 270 };
    public float[] correctRotation;
    [SerializeField]
    bool isPlaced = false;
    int PossibleRots = 1;
    GameManager gameManager;

    private void Awake()
    {
        gameManager = GameObject.Find("GameManager").GetComponent<GameManager>();
    }
    private void Start()
    {
        PossibleRots = correctRotation.Length;
        int rand = Random.Range(0, rotations.Length);
        transform.eulerAngles = new Vector3(0, 0, rotations[rand]);

        if(PossibleRots > 1)
        {
            if (transform.eulerAngles.z == correctRotation[0] || transform.eulerAngles.z == correctRotation[1])
            {
                isPlaced = true;
                gameManager.correctMove();
            }
        }
        else
        {
            if (transform.eulerAngles.z == correctRotation[0])
            {
                isPlaced = true;
                gameManager.correctMove();
            }
        }
    }
    private void OnMouseDown()
    {
        transform.Rotate(new Vector3(0, 0, 90));
        if (PossibleRots > 1)
        {
            if (transform.eulerAngles.z == correctRotation[0] || (transform.eulerAngles.z == correctRotation[1] && isPlaced == false))
            {
                isPlaced = true;
                gameManager.correctMove();
            }
            else if (isPlaced == true)
            {
                isPlaced = false;
                gameManager.wrongMove();
            }
        }
        else
        {
            if (transform.eulerAngles.z == correctRotation[0]  && isPlaced == false)
            {
                isPlaced = true;
                gameManager.correctMove();
            }
            else if (isPlaced == true)
            {
                isPlaced = false;
                gameManager.wrongMove();
            }
        }
        
    }
}
```

Вывод: в ходе проделанной работы была разработана игра Puzzle Plumber

[ЛР17. Разработка игры Puzzle Plumber.zip](https://github.com/Kramler3/LR17/files/10135404/17.Puzzle.Plumber.zip)

