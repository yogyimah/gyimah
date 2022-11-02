# gyimah
Public Class Form1
    Const SALES_TAX As Decimal = 0.05D
    Const PAINT_TOUCH_UP_EXTERIOR As Decimal = 250D
    Const Under_Coat_Extra As Decimal = 300D
    Const Both_UnderCoat_Paint As Decimal = 550D
    Dim New_TIRES As Decimal = 450D
    Dim NEW_HD_RADIO_RATE As Decimal = 190.95D
    Dim BUILT_IN_GPS_RATE As Decimal = 700D
    Dim NEW_FLOOR_MAT_RATE As Decimal = 55D
    Dim VehicleCount_RATE As Integer = 0
    Dim TotalSales_RATE As Decimal = 0
    Dim AVERAGE_RATE As Decimal
    Dim TOTAL_DUE As Decimal
    Const WHOLESALEDISCOUNT As Decimal = 0.2D


    Private Sub ComputeButton_Click(sender As Object, e As EventArgs) Handles ComputeButton.Click

        'Declaring of Variables
        Dim Sub_Total As Decimal
        Dim LOT_NUMBER As Integer
        Dim YEAR As Integer
        Dim VEHICLEMAKE_OR_MODEL As String
        Dim Price As Integer
        Dim TRADE_IN As Decimal
        Dim BUILT_IN_GPS As Decimal
        Dim NEW_TIRE_EXTRA As Decimal
        Dim EXTRA_ONE As Decimal
        Dim EXTRA_TWO As Decimal
        Dim Total_Extra As Decimal
        Dim Discount As Decimal = 0.0
        Dim SALES_TAX As Decimal
        Dim new_floor_extra As Decimal
        Dim NEW_HD_RADIO_EXTA As Decimal


        Try

            LOT_NUMBER = Integer.Parse(LotNumberTextBox.Text, Globalization.NumberStyles.Integer)
            YEAR = Integer.Parse(YearTextBox.Text, Globalization.NumberStyles.Number)
            VEHICLEMAKE_OR_MODEL = VehicleModeTextBox.Text.ToString
            Price = Double.Parse(PriceTextBox.Text, Globalization.NumberStyles.Currency)
            TRADE_IN = Double.Parse(TradeInTextBox.Text, Globalization.NumberStyles.Currency)

            If NewFloorMarCheckBox.Checked = True Then
                new_floor_extra = NEW_FLOOR_MAT_RATE
            Else
                new_floor_extra = 0.0
            End If

            If BuildInCheckBox4.Checked = True Then
                BUILT_IN_GPS = BUILT_IN_GPS_RATE
            Else
                BUILT_IN_GPS = 0.0
            End If

            If NewTiresCheckBox.Checked = True Then
                NEW_TIRE_EXTRA = New_TIRES
            Else
                NEW_TIRE_EXTRA = 0.0
            End If
            If HDCheckBox.Checked = True Then
                NEW_HD_RADIO_EXTA = NEW_HD_RADIO_RATE
            Else
                NEW_HD_RADIO_EXTA = 0.0


            End If



            If Whole_Sale_checkBox.Checked = True Then
                Discount = Price * WHOLESALEDISCOUNT
                EXTRA_ONE = new_floor_extra + NEW_TIRE_EXTRA + BUILT_IN_GPS + NEW_HD_RADIO_EXTA
                Sub_Total = Price + EXTRA_ONE - Discount
                SALES_TAX = 0.0
            Else
                Sub_Total = Price + new_floor_extra + NEW_TIRE_EXTRA + BUILT_IN_GPS + NEW_HD_RADIO_EXTA

            End If

            If PaintUpRadioButton.Checked = True Then
                Sub_Total += PAINT_TOUCH_UP_EXTERIOR
                EXTRA_TWO = PAINT_TOUCH_UP_EXTERIOR
            ElseIf UnderCoatRadioButton.Checked = True Then
                Sub_Total += Under_Coat_Extra
                EXTRA_TWO = Under_Coat_Extra
            ElseIf BothRadioButton.Checked = True Then
                Sub_Total += Both_UnderCoat_Paint
                EXTRA_TWO = Both_UnderCoat_Paint

            Else
                Sub_Total += 0.0
                EXTRA_TWO = 0.0
            End If
            If Whole_Sale_checkBox.Checked = True Then
                SALES_TAX = 0.0
            Else
                SALES_TAX = Sub_Total * SALES_TAX


            End If

            TOTAL_DUE = Sub_Total + SALES_TAX - TRADE_IN
            Total_Extra = EXTRA_ONE + EXTRA_TWO
            Discount_TextBox.Text = Discount.ToString
            Extra_TextBox.Text = Total_Extra.ToString
            SubTotal_TextBox.Text = Sub_Total.ToString
            SalesTextBox.Text = SALES_TAX.ToString
            TotalDueTextBox.Text = TOTAL_DUE.ToString


        Catch ex As MissingFieldException
            MessageBox.Show("Please ensure all fields Has been Field")
        Catch ex As FormatException
            If IsNumeric(PriceTextBox.Text) = False Or PriceTextBox.Text = "" Then
                MessageBox.Show("Please check Price Text Box")

            End If
            If YearTextBox.Text = "" Then
                MessageBox.Show("Please INPUT YEAR")
            End If

        Catch ex As Exception
            MessageBox.Show("Please an error occur" & ex.ToString)

        End Try






    End Sub

    Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load

    End Sub

    Private Sub ColorsToolStripMenuItem_Click(sender As Object, e As EventArgs) Handles ColorsToolStripMenuItem.Click
        ColorDialog1.Color = Me.BackColor
        ColorDialog1.ShowDialog()
        Me.BackColor = ColorDialog1.Color


    End Sub

    Private Sub FontsToolStripMenuItem_Click(sender As Object, e As EventArgs) Handles FontsToolStripMenuItem.Click
        FontDialog1.Font = Me.Font
        FontDialog1.ShowDialog()
        Me.Font = FontDialog1.Font
    End Sub

    Private Sub ExitButton_Click(sender As Object, e As EventArgs) Handles ExitButton.Click
        Dim Message As String = "Do you want to Exit?"
        If MessageBox.Show(Message, "Close Form", MessageBoxButtons.YesNo, MessageBoxIcon.Question) = Windows.Forms.DialogResult.Yes Then
            Me.Close()

        End If
    End Sub

    Private Sub ExitToolStripMenuItem_Click(sender As Object, e As EventArgs) Handles ExitToolStripMenuItem.Click
        ExitButton.PerformClick()
    End Sub

    Private Sub ComputeToolStripMenuItem_Click(sender As Object, e As EventArgs) Handles ComputeToolStripMenuItem.Click
        ComputeButton.PerformClick()
    End Sub

    Private Sub ResetButton_Click(sender As Object, e As EventArgs) Handles ResetButton.Click
        If TOTAL_DUE <> 0 Then
            VehicleCount_RATE += 1
            TotalSales_RATE += TOTAL_DUE
            AVERAGE_RATE = TotalSales_RATE / VehicleCount_RATE
        End If
        TOTAL_DUE = 0.0

        LotNumberTextBox.Clear()
        VehicleModeTextBox.Clear()
        YearTextBox.Clear()
        PriceTextBox.Clear()
        Whole_Sale_checkBox.Checked = False
        Discount_TextBox.Clear()
        Extra_TextBox.Clear()
        SubTotal_TextBox.Clear()
        SalesTextBox.Clear()
        TotalDueTextBox.Clear()
        TradeInTextBox.Clear()
        PaintUpRadioButton.Checked = False
        NoneRadioButton.Checked = True
        UnderCoatRadioButton.Checked = False
        BothRadioButton.Checked = False
        NewTiresCheckBox.Checked = False
        HDCheckBox.Checked = False
        NewFloorMarCheckBox.Checked = False
        BuildInCheckBox4.Checked = False

    End Sub

    Private Sub ResetToolStripMenuItem_Click(sender As Object, e As EventArgs) Handles ResetToolStripMenuItem.Click
        ResetButton.PerformClick()
    End Sub

    Private Sub TotalButton_Click(sender As Object, e As EventArgs) Handles TotalButton.Click
        If VehicleCount_RATE = 0 And TotalSales_RATE = 0 Then
            Dim Message = "No Vehicle has been sold yet"
            MessageBox.Show(Message, "Zero Sales Averages", MessageBoxButtons.OK, MessageBoxIcon.Information)

        Else
            Dim Message =
            MessageBox.Show("Total due all sales: $" & TotalSales_RATE.ToString & ControlChars.NewLine & "Total vehicle sold:" & VehicleCount_RATE & ControlChars.NewLine & "Average total due: $" & AVERAGE_RATE.ToString & MessageBoxIcon.Information, "Totals and Average")

        End If

    End Sub

    Private Sub TotalsToolStripMenuItem_Click(sender As Object, e As EventArgs) Handles TotalsToolStripMenuItem.Click
        TotalButton.PerformClick()
    End Sub
End Class
