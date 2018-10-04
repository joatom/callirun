let gameover = false
let tilt = false
let farbwechsel = 0
let flugdist = 0
let farben: number[] = [Colors.Purple, Colors.Blue, Colors.Green, Colors.Yellow, Colors.Orange, Colors.Red]
let aktFarbe: number = 0
let ticker: number = 0
let hoehe = 0
let luecke = 2
let lauf = 1
let punkte = 0
let kleineLuecken = [12, 25, 34, 43, 48, 53]
let im: Image = images.createBigImage(`
. . . . . . . . . . . . . # . . . . . . . . . . . . # . . . . . . . . # . . . . . . . . # . . . . # . . . . # . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # #
`)

function farbIntervall(farbe: Colors, tick: number) {
    if ((tick >= 0 && tick < 12) ||
        (tick >= 13 && tick < 25) ||
        (tick >= 26 && tick < 34) ||
        (tick >= 35 && tick < 43) ||
        (tick >= 44 && tick < 48) ||
        (tick >= 49 && tick < 53) ||
        (tick >= 54 && tick < 58) ||
        (tick >= 59)
    ) {
        basic.setLedColor(farbe)
    } else {
        basic.setLedColor(0)
    }
}

function gfx(tick: number, luecke: number, yhoehe: number) {

    im.setPixel(tick + 1, 4 - yhoehe, true)

    // naechste Farbe
    if (luecke <= 3) {
        im.setPixel(tick + 4, 4, false)
    }
    if (luecke <= 2) {
        im.setPixel(tick + 3, 4, false)
    }
    if (luecke <= 1) {
        im.setPixel(tick + 2, 4, false)
    }
    if (luecke <= 0) {
        im.setPixel(tick + 1, 4, false)

    }
    im.plotImage(tick);

    im.setPixel(tick + 1, 4 - yhoehe, false)
    if (luecke <= 3) {
        im.setPixel(tick + 4, 4, true)
    }
    if (luecke <= 2) {
        im.setPixel(tick + 3, 4, true)
    }
    if (luecke <= 1) {
        im.setPixel(tick + 2, 4, true)
    }
    if (luecke <= 0) {
        im.setPixel(tick + 1, 4, true)
    }
}


basic.forever(() => {
    if (!gameover) {
        if (input.buttonIsPressed(Button.B) && flugdist < 15) {
            flugdist += 1
            if (hoehe < 4) {
                hoehe += 1
            }
        } else if ((!(input.buttonIsPressed(Button.B)) || flugdist >= 15) && (hoehe > 0 || hoehe == 0 && ticker > 58)) {
            hoehe += -1
        }
        if (hoehe == 0 && kleineLuecken.indexOf(ticker) != -1) {
            punkte++;
        }
        if (hoehe == 0 && ticker < 58) {
            flugdist = 0
        } else if (hoehe < 0) {
            gameover = true
        }
        basic.pause(125 - 5 * lauf)
        ticker += 1
        if (ticker > 58 + luecke) {
            // naechste Farbe
            ticker = 0
            aktFarbe = (aktFarbe + 1) % 6
            switch (aktFarbe) {
                case 0:
                    luecke = 2;
                    break;
                case 1:
                    luecke = 4;
                    break;
                case 2:
                    luecke = 7;
                    break;
                case 3:
                    luecke = 10;
                    break;
                case 4:
                    luecke = 13;
                    break;
                case 5:
                    luecke = 15;
                    break;
            }
            farbwechsel += 1
            if (farbwechsel % 6 == 0) {
                lauf += 1
            }
        }
        gfx(ticker, 58 + luecke - ticker, hoehe);
        farbIntervall(farben[aktFarbe], ticker + 4);
    }
    else if (!tilt) {
        basic.showString("Score: " + punkte + ". GAME OVER! ")
    }
})

input.onGesture(Gesture.Shake, () => {
    tilt = true
    basic.setLedColor(0)
    led.stopAnimation()
    if (!gameover) {
        basic.showString("TILT")
    }
    resetCallirun()
})

function resetCallirun() {
    luecke = 2
    lauf = 1
    punkte = 0
    farbwechsel = 0
    flugdist = 0
    aktFarbe = 0
    ticker = 0
    hoehe = 0
    im = images.createBigImage(`
. . . . . . . . . . . . . # . . . . . . . . . . . . # . . . . . . . . # . . . . . . . . # . . . . # . . . . # . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . .
. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # # #
`)
    gameover = false
    tilt = false
}
