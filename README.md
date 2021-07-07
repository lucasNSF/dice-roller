# dice-roller
Este é meu segundo programa utilizando a linguagem Kotlin e a IDE Android Studio. 😀

O programa consiste no usuário apertar um botão e, a partir deste evento, um dado será lançado caindo em um número aleatório.
Para fazer esse programa foram realizadas as seguintes etapas:

1 - **Criando o layout do app:**
  * Adicionei um `buttom` na `activity_main.xml`, devidamente linkado.
  * Adicionei uma `Image View`, devidamente linkada, para mostrar o dado na tela.
  
2 - **Criando a Classe Dado:**
  * Criei a classe `Dice()` para ser o molde do nosso objeto _dado_. Como nosso dado é um dado comum, os números iriam variar de forma aleatória de 1 a 6 (quantidade de faces do dado).
  ~~~
  class Dice(private val numSides: Int) {

    fun roll(): Int {
        return (1..numSides).random()
    }
}
~~~
3- **Adicionando ação ao botão:**
  * Guardei o id do `buttom` em uma variável `rollButtom` que ficará escutando um evento de clique nela mesma, e após esse evento,
  executará a função de lançar o dado (função chamada de `rollDice()`). A função `rollDice()` é executada ao menos 1 vez para
  assegurar que uma imagem de dado será mostrada ao iniciar o app.
  ~~~
  val rollButton: Button = findViewById(R.id.button)
        rollButton.setOnClickListener { rollDice() }

        rollDice()
  ~~~
  * Finalmente criei a função `rollDice()`. Na qual possui um objeto `dice` no padrão de 6 lados e uma outra variável para armazenar o valor aleatório gerado pelo método
  `roll()` da classe `Dice`. A partir deste valor armazenado, é executada uma estrutura de controle de decisão na qual mostra a imagem correspondente do valor do dado após ser
  lançado.
  ~~~
  private fun rollDice() {
        // Cria um novo objeto Dado e o joga
        val dice = Dice(6)
        val diceRoll = dice.roll()
        val diceImage : ImageView = findViewById(R.id.imageView)

        val drawableResource = when (diceRoll) {
            1 -> R.drawable.dice_1
            2 -> R.drawable.dice_2
            3 -> R.drawable.dice_3
            4 -> R.drawable.dice_4
            5 -> R.drawable.dice_5
            else -> R.drawable.dice_6
        }
        diceImage.setImageResource(drawableResource)
        diceImage.contentDescription = diceRoll.toString()
    }
