# project
project
PrintWriter pw=response.getWriter();
		String search=request.getParameter("search");
		try {
			Class.forName("com.mysql.jdbc.Driver");
			Connection con=DriverManager.getConnection("jdbc:mysql://localhost:3306/project","root","root");
			PreparedStatement pst;
			RequestDispatcher rd;
			ResultSet rst;
		if (search.equals("labor"))
		{
			pst=con.prepareStatement("select *from workers");
			rst=pst.executeQuery();
			rd=request.getRequestDispatcher("worker.html");
			rd.forward(request, response);
			
		}
		else if(search.equals("storage"))
		{
			pst=con.prepareStatement("select *from storage");
			rst=pst.executeQuery();
			rd=request.getRequestDispatcher("storage.html");
			rd.forward(request, response);
		}
		else {
		
			 pst=con.prepareStatement("select sname,loc,cost from products where ename=?");
			pst.setString(1, search);
			 rst=pst.executeQuery();
			
			if(rst==null)
			{
				pw.println("product not found");
				rd=request.getRequestDispatcher("home.html");
				rd.include(request, response);
				
			}
			else {
				rd=request.getRequestDispatcher("product.html");
				rd.forward(request, response);
			}
			
		}
		}
		catch(Exception e)
		{
			e.printStackTrace();
		}
