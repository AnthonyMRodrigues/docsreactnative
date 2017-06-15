## Alinhamento de Pixels na Grade

No iOS, você pode especificar as posições e as dimensões para os elementos com uma precisão arbitrária qualquer; por exemplo 29.674825. Porém, contudo, o display físico tem somente um número fixo de pixels; por exemplo 640×960 para o iPhone 4 ou 750×1334 para o iPhone 6. O iOS tenta ser tão fiel quanto possível ao valor do usuário ao propagar um pixel originário em múltiplos para enganar o olho. A desvantagem desta técnica é que ela faz com que o elemento assim obtido pareça borrado.

Na prática, descobrimos que os desenvolvedores não querem esta funcionalidade, e que eles têm que trabalhar em torno disto fazendo arredondamento manual no intuito de evitar de ter os elementos borrados. No React Native, estamos arredondando todos os pixels automaticamente.

Temos que ser cuidadosos quando fizermos este arredondamento. Você jamais vai querer trabalhar com valores com & sem arredondamento ao mesmo tempo que, à medida que avança, você vai acumulando erros de arredondamento. Mesmo tendo um único erro de arredondamento é mortal, porque uma borda de apenas um pixel pode desaparecer ou acabar ficando duas vezes maior.

No React Native, tudo em JS e dentro do motor de layout trabalham com números arbitrários de precisão. É somente quando definimos as posições e as dimensões do elemento nativo no thread principal é que nós arredondamos. Além disso, o arredondamento é feito relativo à raiz ao invés do progenitor; novamente para evitar de se acumular erros de arredondamento.
