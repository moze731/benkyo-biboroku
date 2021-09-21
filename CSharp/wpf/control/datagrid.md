# DataGrid

## DataGridの宣言

## DataGrid.ItemContainerStyle

DataGridの各行のスタイルを設定するのに、`DataGrid.ItemContainerStyle`を使用する。

以下の例は、`Control`という列挙型のプロパティにより、行の`BackGround`を変更している。

```C#

<DataGrid>
    <DataGrid.ItemContainerStyle>
        <Style TargetType="DataGridRow">
            <Style.Triggers>
                <DataTrigger Binding="{Binding Control.Value}" Value="None">
                    <Setter Property="Background" Value="white" />
                </DataTrigger>
                <DataTrigger Binding="{Binding Control.Value}" Value="Add">
                    <Setter Property="Background" Value="Cyan" />
                </DataTrigger>
                <DataTrigger Binding="{Binding Control.Value}" Value="Update">
                    <Setter Property="Background" Value="Cyan" />
                </DataTrigger>
                <DataTrigger Binding="{Binding Control.Value}" Value="Delete">
                    <Setter Property="Background" Value="LightSalmon" />
                </DataTrigger>
            </Style.Triggers>
        </Style>
    </DataGrid.ItemContainerStyle>
</DataGrid>  

```

## DataGridTemplateColumn

DataGridColumnsのコンテンツとして、宣言できる列の型の一つ。
通常時の表示を、`CellTemplate`、編集時の表示を、`EditingCellTemplate`で指定する。

以下の例はCellTemplateは`TextBlock`で3桁区切りに数値を表示し、`EditingCellTemplate`は`TextBox`で文字入力を可能にしている。また、TextBoxは別途定義してる`NumericTextBoxBehavior`により、数値のみを入力可能にしている。

```C#
<DataGrid>
    <DataGridColomns>
        <DataGridTemplateColumn Header="合計金額" MinWidth="50">
            <DataGridTemplateColumn.CellTemplate>
                <DataTemplate>
                    <TextBlock Text="{Binding Cash, StringFormat={}{0:N0}}"
                               Background="Transparent" />
                </DataTemplate>
            </DataGridTemplateColumn.CellTemplate>
            <DataGridTemplateColumn.CellEditingTemplate>
                <DataTemplate>
                    <TextBox Text="{Binding Cash}" BorderThickness="0">
                        <i:Interaction.Behaviors>
                            <dc:NumericTextBoxBehavior/>
                        </i:Interaction.Behaviors>
                    </TextBox>
                </DataTemplate>
            </DataGridTemplateColumn.CellEditingTemplate>
        </DataGridTemplateColumn>
    </DataGridColomns>
</DataGrid>
```

**注記**
`CellTemplate`と`EditingCellTemplate`の両方を`TextBox`にすると、`EditingCellTemplate`が反映されない事象が発生。原因不明。