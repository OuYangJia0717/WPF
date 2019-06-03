# WPF
开发wpf

//双击单行事件
private void DataGridRow_MouseDoubleClick(object sender, MouseButtonEventArgs e)
        {
            var row = sender as DataGridRow;
            var info = row?.DataContext as BloodRegisterInformation;
            if (info == null)
            {
                MessageBox.Show("请选中一行数据");
                return;
            }

            if (info.IsLinked == false)
            {
                MessageBox.Show("样本未连接");
                return;
            }
            ViewModel.ExecuteMore(info);
            //过滤控件内事件
            if (e.Source is DataGridRow)
            {
                e.Handled = true;
            }
        }
        
        
//选择DataGrid改变事件
        private void DataGrid_SelectionChanged(object sender, SelectionChangedEventArgs e)
        {
            ViewModel.SelectedInfo = RegisterListDataGrid.SelectedItems;
        }



//选中的DataGrid数据行定义
        private List<BloodRegisterInformation> InfoList;

        public IList SelectedInfo
        {
            get { return InfoList; }
            set { InfoList = value.Cast<BloodRegisterInformation>().ToList(); }
        }
