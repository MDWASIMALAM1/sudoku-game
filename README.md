public class backtrackingsudoku {
   public backtrackingsudoku() {
   }

   public boolean issafe(char[][] var1, int var2, int var3, int var4) {
      int var5;
      for(var5 = 0; var5 < var1.length; ++var5) {
         if (var1[var5][var3] == (char)(var4 + 48)) {
            return false;
         }

         if (var1[var2][var5] == (char)(var4 + 48)) {
            return false;
         }
      }

      var5 = var2 / 3 * 3;
      int var6 = var3 / 3 * 3;

      for(int var7 = var5; var7 < var5 + 3; ++var7) {
         for(int var8 = var6; var8 < var6 + 3; ++var8) {
            if (var1[var7][var8] == (char)(var4 + 48)) {
               return false;
            }
         }
      }

      return true;
   }

   public boolean helper(char[][] var1, int var2, int var3) {
      if (var2 == var1.length) {
         return true;
      } else {
         boolean var4 = false;
         boolean var5 = false;
         int var7;
         int var8;
         if (var3 != var1.length - 1) {
            var7 = var2;
            var8 = var3 + 1;
         } else {
            var7 = var2 + 1;
            var8 = 0;
         }

         if (var1[var2][var3] != '.') {
            if (this.helper(var1, var7, var8)) {
               return true;
            }
         } else {
            for(int var6 = 1; var6 <= 9; ++var6) {
               if (this.issafe(var1, var2, var3, var6)) {
                  var1[var2][var3] = (char)(var6 + 48);
                  if (this.helper(var1, var7, var8)) {
                     return true;
                  }

                  var1[var2][var3] = '.';
               }
            }
         }

         return false;
      }
   }

   public void solvesudoku(char[][] var1) {
      this.helper(var1, 0, 0);
   }
}
