SOURCE = input(hlc3) RSILENGTH = input(14, title = "RSI LENGTH") RSICENTERLINE = input(52, title = "RSI CENTER LINE") MACDFASTLENGTH = input(7, title = "MACD FAST LENGTH") MACDSLOWLENGTH = input(12, title = "MACD SLOW LENGTH") MACDSIGNALSMOOTHING = input(12, title = "MACD SIGNAL SMOOTHING") a = input(1, title = "Key Vaule. 'This changes the sensitivity'") SmoothK = input(3) SmoothD = input(3) LengthRSI = input(14) LengthStoch = input(14) RSISource = input(close) c = input(10, title="ATR Period") xATR = atr(c) nLoss = a * xATR xATRTrailingStop = iff(close > nz(xATRTrailingStop[1], 0) and close[1] > nz(xATRTrailingStop[1], 0), max(nz(xATRTrailingStop[1]), close - nLoss), iff(close < nz(xATRTrailingStop[1], 0) and close[1] < nz(xATRTrailingStop[1], 0), min(nz(xATRTrailingStop[1]), close + nLoss), iff(close > nz(xATRTrailingStop[1], 0), close - nLoss, close + nLoss))) pos = iff(close[1] < nz(xATRTrailingStop[1], 0) and close > nz(xATRTrailingStop[1], 0), 1, iff(close[1] > nz(xATRTrailingStop[1], 0) and close < nz(xATRTrailingStop[1], 0), -1, nz(pos[1], 0))) color = pos == -1 ? red: pos == 1 ? green : blue ema= ema(close,1) above = crossover(ema,xATRTrailingStop ) below = crossover(xATRTrailingStop,ema) buy = close > xATRTrailingStop and above sell = close < xATRTrailingStop and below barbuy = close > xATRTrailingStop barsell = close < xATRTrailingStop plotshape(buy, title = "Buy", text = 'Buy', style = shape.labelup, location = location.belowbar, color= green,textcolor = white, transp = 0, size = size.tiny) plotshape(sell, title = "Sell", text = 'Sell', style = shape.labeldown, location = location.abovebar, color= red,textcolor = white, transp = 0, size = size.tiny) barcolor(barbuy? green:na) barcolor(barsell? red:na) alertcondition(buy, title='Buy', message='Buy') alertcondition(sell, title='Sell', message='Sell')
