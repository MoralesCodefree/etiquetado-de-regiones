

# etiquetado-de-regiones
Etiqueta regiones conectadas(4)

/**
 *
 * @author MoralesCodefree
 */
public class Etiquetado {

    ArrayList numerodeRegiones = new ArrayList();
    ArrayList RegionesyArea = new ArrayList();
    int regionMayor = 0, areaMayor = 0;

    public int[][] barrer(int[][] unamatriz) {
        int[][] nueva_matriz = RECORRER_ARRIBA_ABAJO(
                RECORRER_ABAJO_ARRIBA(
                        RECORRER_ARRIBA_ABAJO(
                                etiquetar(
                                        ponerOrillasEnCero(unamatriz)))));
        contarRegiones(nueva_matriz);
        obtenerArea(nueva_matriz);
        //imprimirRegionesYArea();
        buscaAreasMayor();
        nueva_matriz = eliminarAreasMenores(nueva_matriz);
        
        
        return nueva_matriz;
    }

    public int[][] etiquetar(int[][] matriz) {
        //int contador = 5;
        /**
         * *RECORERMATRIZ AZUL ABAJO HACIA ARRIBA
         */
        for (int i = 1; i < matriz.length - 1; i++) {
            for (int j = 1; j < matriz[0].length - 1; j++) {
                if (matriz[i][j] != 0) {
                    matriz[i][j] = i + j;
                    //contador++;
                }

            }
        }
        //  immprimirMatriiz(matriz);
        return matriz;
    }

    public int[][] RECORRER_ARRIBA_ABAJO(int[][] unamatriz) {
        /**
         * *RECORERMATRIZ DE ARRIBA HACIA ABAJO, IZQUIERDAA DERECHA
         */
        for (int i = 1; i < unamatriz.length; i++) {
            for (int j = 1; j < unamatriz[0].length; j++) {
                if (unamatriz[i][j] != 0) {
                    if (unamatriz[i][j - 1] != 0) {
                        unamatriz[i][j] = unamatriz[i][j - 1];
                    } else if (unamatriz[i - 1][j] != 0) {
                        unamatriz[i][j] = unamatriz[i - 1][j];
                    }
                }

            }
        }

        for (int j = 1; j < unamatriz[0].length; j++) {
            for (int i = 1; i < unamatriz.length; i++) {
                if (unamatriz[i][j] != 0) {
                    if (unamatriz[i - 1][j] != 0) {
                        unamatriz[i][j] = unamatriz[i - 1][j];
                    } else if (unamatriz[i][j - 1] != 0) {
                        unamatriz[i][j] = unamatriz[i][j - 1];
                    }
                }

            }
        }

        return unamatriz;
    }

    public int[][] RECORRER_ABAJO_ARRIBA(int[][] unamatriz) {

        /**
         * *RECORERMATRIZ DE ABAJO HACIA ARRIBA
         */
        for (int j = unamatriz[0].length - 1; j > 0; j--) {
            for (int i = unamatriz.length - 1; i > 0; i--) {
                if (unamatriz[i][j] != 0) {
                    if (unamatriz[i + 1][j] != 0) {
                        unamatriz[i][j] = unamatriz[i + 1][j];
                    } else if (unamatriz[i][j + 1] != 0) {
                        unamatriz[i][j] = unamatriz[i][j + 1];
                    }

                }
            }
        }

        for (int i = unamatriz.length - 1; i > 0; i--) {
            for (int j = unamatriz[0].length - 1; j > 0; j--) {
                if (unamatriz[i][j] != 0) {
                    if (unamatriz[i][j + 1] != 0) {
                        unamatriz[i][j] = unamatriz[i][j + 1];
                    } else if (unamatriz[i + 1][j] != 0) {
                        unamatriz[i][j] = unamatriz[i + 1][j];
                    }

                }
            }
        }

        //immprimirMatriiz(unamatriz);
        return unamatriz;
    }

    public int[][] ponerOrillasEnCero(int[][] matriz) {

        for (int i = 0; i < matriz.length; i++) {
            matriz[i][0] = 0;
            matriz[i][matriz[0].length - 1] = 0;

        }
        System.out.println("Alto: " + matriz.length + " Ancho : " + matriz[0].length);
        for (int j = 0; j < matriz[0].length; j++) {
            matriz[0][j] = 0;
            matriz[matriz.length - 1][j] = 0;

        }
        /// immprimirMatriiz(matriz);
        return matriz;
    }

    public int contarRegiones(int[][] matriz) {

        for (int i = 1; i < matriz.length; i++) {
            for (int j = 1; j < matriz[0].length; j++) {
                if (matriz[i][j] != 0 && !numerodeRegiones.contains(matriz[i][j])) {
                    numerodeRegiones.add(matriz[i][j]);
                }
            }

        }
        return numerodeRegiones.size();
    }

    public void immprimirMatriiz(int[][] matriz) {
        for (int i = 0; i < matriz.length; i++) {
            for (int j = 0; j < matriz[0].length; j++) {
                System.out.print(" " + matriz[i][j]);
            }
            System.out.println("");

        }

    }

    public void obtenerArea(int[][] matriz) {
        int aux = 0;
        int contador = 0;
        for (int k = 0; k < numerodeRegiones.size(); k++) {
            aux = (int) numerodeRegiones.get(k);
            for (int i = 0; i < matriz.length; i++) {

                for (int j = 0; j < matriz[0].length; j++) {

                    if ((int) numerodeRegiones.get(k) == (int) (matriz[i][j])) {
                        contador++;

                    }

                }

            }
            RegionesyArea.add(k, aux + "," + contador);
            contador = 0;
        }

    }

    public void buscaAreasMayor() {
        int mayor = 0, aux = 0;
        String dato = "";
        for (int k = 0; k < RegionesyArea.size(); k++) {
            dato = (String) RegionesyArea.get(k);
            String[] datos = dato.split(",");
            if (aux < Integer.parseInt(datos[1])) {
                aux   = Integer.parseInt(datos[1]);
                mayor = Integer.parseInt(datos[0]);
            }
        }
        regionMayor = mayor;
        areaMayor = aux;
        System.out.println("===>La region es : " + regionMayor + " Tiene El area mayor y  es  :" + areaMayor);

    }

    public int[][] eliminarAreasMenores(int[][] matriz) {
       
        for (int i = 1; i < matriz.length-1; i++) {
            for (int j = 1; j < matriz[0].length-1; j++) {

                if (matriz[i][j] != regionMayor) {
                    matriz[i][j] = 0;
                } else if (matriz[i][j] == regionMayor) {
                    matriz[i][j] = 255;
                }
            }

        }
        
        
        return matriz;
    }

    void imprimirRegionesYArea() {
        String dato = "";
        for (int i = 0; i < RegionesyArea.size(); i++) {
            dato = (String) RegionesyArea.get(i);
            String[] datos = dato.split(",");
            System.out.println("Region " + datos[0] + "  Area: " + datos[1]);

        }

    }

}
