#include <iostream>
#include <boost/config.hpp>
#include <boost/uuid/uuid.hpp>
#include <boost/multi_index_container.hpp>
#include <boost/multi_index/member.hpp>
#include <boost/multi_index/ordered_index.hpp>
#include <boost/multi_index/composite_key.hpp>
#include <boost/multi_index/mem_fun.hpp>
#include <boost/uuid/nil_generator.hpp>
#include <boost/uuid/string_generator.hpp>
#include <boost/uuid/uuid_generators.hpp>
#include <memory>
#include <utility>
#include <cassert>
#include <functional>

using namespace std;
using boost::multi_index_container;
using namespace boost::multi_index;

struct input_stream_info
{
	/* tags for accessing the corresponding indices of input_stream_info set */
	struct by_buffer_id {};
	struct by_source_id {};
	//-----------------------
	//! Input stream buffer id
	BOOST_ALIGNMENT(16) const boost::uuids::uuid m_buffer_id;
	BOOST_ALIGNMENT(16) const boost::uuids::uuid m_source_id;

	boost::uuids::uuid get_source_id()	const {	return m_source_id;	}
	boost::uuids::uuid get_buffer_id()	const {	return m_buffer_id;	}

	//! Default constructor
	explicit input_stream_info(boost::uuids::uuid const& buffer_id, boost::uuids::uuid const& source_id)
		:m_buffer_id(buffer_id),
		 m_source_id(source_id)

	{

	}

	//! Destructor
	~input_stream_info()
	{

	}

	// Copying prohibited
	input_stream_info(input_stream_info const&) = delete;
	input_stream_info& operator= (input_stream_info const&) = delete;
};

using input_stream_list = multi_index_container<input_stream_info*,
	indexed_by<
		ordered_unique<
			tag<input_stream_info::by_buffer_id>, const_mem_fun<input_stream_info, boost::uuids::uuid, &input_stream_info::get_buffer_id>,
			std::less<boost::uuids::uuid>
		>,
		ordered_unique<
			tag<input_stream_info::by_source_id>, const_mem_fun<input_stream_info, boost::uuids::uuid, &input_stream_info::get_source_id>,
			std::less<boost::uuids::uuid>
		>
	>
>;

int main(int argc, char *argv[])
{
	input_stream_list list_stream;
	boost::uuids::uuid source_id_to_find = boost::uuids::nil_uuid();
	for (int i=0; i<10; ++i)
	{
		boost::uuids::uuid buffer_id = boost::uuids::random_generator()();
		boost::uuids::uuid source_id = boost::uuids::random_generator()();
		if (i == 5)
		{
			source_id_to_find = source_id;
		}
		input_stream_info* p_stream = new input_stream_info(buffer_id, source_id);
		list_stream.insert(p_stream);
	}
	//-- try to find to it --
	input_stream_info* p_info = nullptr;
	const auto & ls = list_stream.get<input_stream_info::by_source_id>();
	auto it = ls.find(source_id_to_find);
	if (it != ls.end())
	{
		p_info = *it;
		
	}
	if (p_info != nullptr ) 
	{
	    std::cout << "was find" << endl;	    
	}
	for (auto& stream: list_stream)
	{
	    delete &stream;
	}
	list_stream.clear();
	return 0;
}
