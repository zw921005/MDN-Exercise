# BizSmobiler

## FAQ
- 点击按钮报**网络无响应**


smobiler默认方法执行10S后超时，需增加**ShowLoadingScreen()**、**CloseLoadingScreen()**，例子：

```visual basic
''' <summary>
''' 保存
''' </summary>
''' <param name="sender"></param>
''' <param name="e"></param>
Private Sub Btn_Save_Press(sender As Object, e As EventArgs) Handles Btn_Save.Press
    MessageBox.Show("确定要创建当前的物料主数据维护吗?", MessageBoxButtons.OKCancel,
    Sub(s As Object, args As MessageBoxHandlerArgs)
    Try
        If args.Result = ShowResult.OK Then
            ShowLoadingScreen()
            Dim obj As New SearchingSCECore.Material(Client.UserSessionID)
            SaveData()
            data = obj.Create(data).Data
            Toast("创建成功")

            If type = AddNewType.copyAddNew Then
                Me.prevForm.data = data
                Me.prevForm.isModify = True
                Me.prevForm.Refresh()
                Me.Close()
            Else
                Me.prevForm.isAddNew = True
                Me.prevForm.detailData = data
                Me.Close()
            End If
        End If
    Catch ex As Exception
        MessageBox.Show(ex.Message)
    Finally
        CloseLoadingScreen()
    End Try
    End Sub)
End Sub
```
