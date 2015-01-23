# How-to-fit-uiwebview-into-uitableviewcell
many people has a problem that the height of UIWebView can't achieve in the UITableViewCell
First of all,We must achieve UIWebViewDelegate,and We'd better prepare a UIWebView to calculate the height of the webview that you using in interface.
WARNING:You'd better build a webview that calculate height in UITableViewCell.
Now,The Code for Example

NSData *database64 = [[NSData alloc]initWithBase64EncodedString:[dataArray objectForKey:@"content"] options:0];
            item.content = [[NSString alloc]initWithData:database64 encoding:NSUTF8StringEncoding];
            item.picurl = [dataArray objectForKey:@"picurl"];
            item.time = [dataArray objectForKey:@"createtime"];
            item.replyArray = [dataArray objectForKey:@"reply"];
            
            [calculateCell.calculateWebView loadHTMLString:item.content baseURL:[NSURL fileURLWithPath:[[NSBundle mainBundle] bundlePath]]];
            calculateCell.calculateWebView.delegate = self;  //the calculateCell.calculateWebView is UIWebView is calculated the web height;
            
            
-(void)webViewDidFinishLoad:(UIWebView *)webView{
    NSString *height_str= [webView stringByEvaluatingJavaScriptFromString: @"document.body.offsetHeight"];
    webheight = [height_str floatValue];
    [_tableview reloadData];
}
When we get the height,we can reloadData.
