# weare
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace WindowsFormsApp1
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }


        private String rbc()
        {
            System.Net.WebClient wc = new System.Net.WebClient();
            String Response = wc.DownloadString("https://nsk.rbc.ru/");
            //<span class="indicators__td indicators__sum">64,17</span>
            String Rate = System.Text.RegularExpressions.Regex.Match(Response, @"<span class=""indicators__td indicators__sum"">([0-9]+\,[0-9]+)</span>").Groups[1].Value;
            return "РБК: " + Rate + " р.\r\n";
        }
        private String cb()
        {
            System.Net.WebClient wc = new System.Net.WebClient();
            String Response = wc.DownloadString("https://www.cbr.ru/");
            //  <ins class="rubl">руб.</ins>&nbsp;64,4993</td>

            String Rate = System.Text.RegularExpressions.Regex.Match(Response, @"</ins>&nbsp;([0-9]+\,[0-9]+)</td>").Groups[1].Value;
            return "ЦБ: " + Rate + " р. \r\n";
        }

        private void Form1_Shown(object sender, EventArgs e)
        {
            textBox2.Text = rbc() + cb() ;
        }
    }
}
