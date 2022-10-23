
# Relógio, Temporizador e Cronômetro

> Status: Concluded

## Relogio

<img src="https://i.postimg.cc/prgzH5Yy/bank-small.png" alt="bank-small" width="100%">

Aplicação desenvolvida afim de aprender Svelte, ao qual foi utilizado o SvelteKit, criando um Relógio, com a função padrão de horas, temporizador e cronômetro.

# Desenvolvimento

Desenvolvido com SvelteKit, funções realizadas com lógica de programação.

* Relógio

```js
    let horasRelogio = '00';
    let minutosRelogio = '00';
    let segundosRelogio = '00';
    
    function formatDigit(digit: string) {
        if(parseInt(digit) < 10) {
            digit = '0'+digit;
            return digit;
        } else {
            return digit;
        }
    }

    const relogio = setInterval(() => {
        let dateToday = new Date();
        horasRelogio = formatDigit(dateToday.getHours().toString());
        minutosRelogio = formatDigit(dateToday.getMinutes().toString());
        segundosRelogio = formatDigit(dateToday.getSeconds().toString());
    })
```

#

* Cronômetro

```js
    let horas = 0;
    let minutos = 0;
    let segundos = 0;

    let horasCronometro = '00';
    let minutosCronometro = '00';
    let segundosCronometro = '00';

    function formatDigit(digit: string) {
        if(parseInt(digit) < 10) {
            digit = '0'+digit;
            return digit;
        } else {
            return digit;
        }
    }

    function Cronometro() {
        segundos++;

        if(segundos === 60) {
            segundos = 0;
            minutos++;

            if(minutos === 60) {
                segundos = 0;
                minutos = 0;
                horas++;
            }
        }

        return [horasCronometro = formatDigit(horas.toString()), minutosCronometro = formatDigit(minutos.toString()), segundosCronometro = formatDigit(segundos.toString())];
    }
```

#

* Temporizador

```js
    let horasTemporizador = '00';
    let minutosTemporizador = '00';
    let segundosTemporizador = '00';

    let horas = 0;
    let minutos = 0;
    let segundos = 0;

    function formatDigit(digit: string) {
        if(parseInt(digit) < 10) {
            digit = '0'+digit;
            return digit;
        } else {
            return digit;
        }
    }

    function Temporizador() {
        if(segundos === 0) {
            segundos = 60;

            if(minutos === 0) {
                minutos = 60;

                if(horas === 0) {
                    isPiscando = true;
                    setTimeout(() => {
                        isPiscando = false;
                    }, 3000);
                    document.querySelector<any>('audio').play();
                    clearInterval(interval);
                    ResetTemporizador();
                } else {
                    horas -= 1;
                }
            } else {
                minutos -= 1;
            }
        } else {
            segundos--;
        }

        return [horasTemporizador = formatDigit(horas.toString()), minutosTemporizador = formatDigit(minutos.toString()), segundosTemporizador = formatDigit(segundos.toString())];
    }

```
